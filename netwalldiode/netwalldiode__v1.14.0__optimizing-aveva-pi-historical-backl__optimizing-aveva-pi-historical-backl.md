<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl -->

# Optimizing AVEVA Pi Historical Backfill

## <Description>

This section provides a description of how NetWall's AVEVA Pi Historical Backfill feature works as well as how it can be tuned to optimize performance.

NetWall AVEVA Pi-Blue will read historical values from the Blue PI system for each point in which we have interest and send those values across MetaDefender Optical Diode. The data block from Blue also contains the starting and ending time of the query made by NetWall AVEVA Pi-Blue. NetWall AVEVA Pi-Red receives the historical values from NetWall AVEVA Pi-Blue and then issues a historical data query of the PI database using the starting and ending time stated in the data block from NetWall AVEVA Pi-Blue. NetWall AVEVA Pi-Red then compares the result of its query with the data block from NetWall AVEVA Pi-Blue. If a value from NetWall AVEVA Pi-Blue is missing on NetWall AVEVA Pi-Red then PI-Red writes that value to the Red PI Archive. If a value from NetWall AVEVA Pi-Blue is already present on NetWall AVEVA Pi-Red then PI-Red takes no action.

If HistoryTimeSpan is 0, no history collection will take place. If AllowHistoryDelete is *not* 0, then history backfill on Red is allowed to delete historical values present in the Red PI archives that are not present on Blue. If AllowHistoryDelete is 0, then history backfill can only add values to the Red PI Archives: no values are deleted from the Red PI Archives.

The user specifies a backfill time span (i.e., the last 4hours). NetWall AVEVA Pi-Blue extracts history starting at the current real time, ending at a previous time (current real time minus the backfill time span.) NetWall AVEVA Pi-Blue will cycle through all of the historical data for the points of interest and then start the cycle over again, with current real time being the start time.

Note that the most recent 30 minutes of historical data will not be read from Blue. This is to avoid issues with exception and compression processing by Aveva PI.

## [Switching to Standard Time from Daylight Savings Time](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#switching-to-standard-time-from-daylight-savings-time)

In early spring (March), many time zones advance the clock by 1 hour at 2AM when switching from Daylight Savings time to Standard Time. When the time on the computer hosting Aveva PI is advanced, the Aveva PI system will notice that time has been adjusted. In this case, it has adjusted one hour into the future. So, essentially, there is a hole in the PI database between 2AM and 3AM on the day that the clocks were advanced.

The NetWall AVEVA Pi-Blue system performs queries of the PI archives for historical backfill, as described in the previous section. However, when a historical query is attempted for a time when the clock was changed (i.e., between 2AM and 3AM) the Aveva PI SDK throws an exception, and no historical data is processed.

Note that the OPSWAT PI-Blue system will continue to operate but may not be able to backfill data if any of the starting/ending times of the backfill cycle fall within the hole created by the advancing of the clock.

If you need to backfill any data that occurred either before or after the 2AM – 3AM hole, use the partial backfill function. Make sure, however, that the starting or ending times for the partial backfill do not encroach on the 2AM-3AM hole or PI will throw an exception and no data will be processed.

## [Suggested starting parameters](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#suggested-starting-parameters)

OPSWAT suggest to start with the folowing parameters:

- Backfill Time: 4 hours
- History slice: 60 minutes
- Max values per second: 5000

With these parameters, NetWall AVEVA Pi-Blue will read successive 60-minute blocks of historical data for each point of interest. Note that the most recent 30 minutes of history will not be read from NetWall Blue. This avoids possible conflicts with exception and compression processing by PI.

The result of each 60-minute read will be sent as a block to NetWall AVEVA Pi-Red. If 5000 values are sent in less than a second, NetWall AVEVA Pi-Blue will pause the History Read operation for the remainder of the second. It will only send full reads, so if a 60-minute block contains 30,000 values, all those values will be sent to NetWall AVEVA Pi-Red regardless of the Max values per second parameter.

## [Potential Historical Data Issues when using Diodes](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#potential-historical-data-issues-when-using-diodes)

NetWall AVEVA Pi-Blue collects historical data as described in the Description section above and sends it to Red. NetWall AVEVA Pi-Blue is constrained by the maximum number of values per second that it is allowed to send to Red. If NetWall AVEVA Pi-Blue is unable to complete an entire history cycle in less time than the specified History Time Span, then a *History Overrun* condition exists.

NetWall AVEVA Pi-Red buffers up to 5,000 historical data blocks from NetWall AVEVA Pi-Blue and processes each data block as described in the Description section above. If NetWall AVEVA Pi-Red is unable to process the data blocks at the rate they are received from NetWall AVEVA Pi-Blue, a *Buffer Overrun* condition is created in NetWall AVEVA Pi-Red. When Buffer Overrun occurs, NetWall AVEVA Pi-Red discards all the pending 5000 data blocks from its buffers.

Counters keep track of the number of buffer & history overruns and is displayed to the user on the Netwall Stats page for the Aveva PI interface. They are also logged into Syslog and into the Windows Event log where the OPSWAT PI interfaces are running. Each increment of the Buffer Overrun counter represents an overflow of 5000 NetWall AVEVA Pi-Blue history data blocks. Each increment of the History Overrun counter represents one Blue History Backfill cycle that had an overrun.

## [Tuning Historical Backfill for best results](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#tuning-historical-backfill-for-best-results)

There are two conditions that will create issues:

- **Blue History Overrun** (History too slow)

  - Increase Blue Max Values per Second.
  - Increase Blue History Slice.
- **Red Buffer Overrun** (History too fast):

  - Increase Blue History Slice.
  - Decrease Blue Max Values per Second.

### [Blue History Slice](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#blue-history-slice)

Increasing the Blue History Slice will make both Blue and Red run more efficiently: PI performs better with fewer calls of longer time ranges than many calls of lesser time ranges.

Try adding one hour to the Blue History Slice and observe the History Per Second statistic on Blue for about 5 minutes. If your rate is consistently about the same as your History Max Values Per Second, then you can leave the Blue History Slice as it is or add an additional 30 minutes to the Blue History Slice and repeat your observation.

If History Per Second is consistently exceeding History Max Values Per Second by 25% or more, then reduce the Blue History Slice by 15 minutes and try again.

### [Increase/Decrease Blue Max Values Per Second](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#increasedecrease-blue-max-values-per-second)

#### [Blue History Overrun](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#blue-history-overrun)

In this case, NetWall AVEVA Pi-Blue is not getting data fast enough from the Blue PI server.

You must increase Blue Max Values Per Second to increase the quantity of historical data flowing from Blue to Red. Increase Blue Max Values Per Second by 5000 and increase the Blue History Slice as described in the previous section. Observe the Blue History Overrun statistic after two History Cycles and verify the counter is no longer incrementing. Also observe the Red Buffer Overrun statistic to make sure you are not driving Red too hard.

- The Blue History Cycles statistic will increment at the end of a complete Blue History Cycle.
- The Blue Current History Pct Complete is the percentage complete for the current History Cycle.
- The Blue Current History Elapsed Time is the amount of time elapsed so far in the current History Cycle.

#### [Red Buffer Overrun](/docs/netwalldiode/v1.14.0/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#red-buffer-overrun)

In this case, NetWall AVEVA Pi-Red receives data from NetWall AVEVA Pi-Blue faster than it can be placed into the Red PI database. The Red Buffer Overrun statistic on Red will increase every time the PI-Red History buffer exceeds 5000 Blue History Blocks

- Make sure you have optimized the Blue History Slice as described in the previous section. If not, then follow that procedure and see if Red Buffer Overrun no longer increments.
- Decrease the Blue Max Values Per Second by about 2500 values at a time, and see if Red Buffer Overrun no longer increments.

If you must decrease the Blue Max Values Per Second to the point that you start getting Blue History Overrun, then you will probably need to increase the resources of your Red PI Server. If the Server is running virtually, you may need to assign more memory/CPU to the Red PI Server.

Review the PI-Red Syslog and look for patterns of when you are experiencing the Red Buffer Overrun. You may have some action that is running periodically (file backup, etc.) that is consuming all of the resources of the PI Server machine.

MetaDefender
