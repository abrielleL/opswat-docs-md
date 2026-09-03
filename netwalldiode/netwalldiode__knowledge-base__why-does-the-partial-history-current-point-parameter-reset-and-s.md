<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/why-does-the-partial-history-current-point-parameter-reset-and-s -->

# Why does the partial history current point parameter reset and start over again every so often?

This article applies to all Metadefender Optical Diode versions configured on High Availability Mode

The Partial History Current Point parameter will keep increasing until it reaches the value of the Partial History Total Points parameter. Then, it will reset itself and start over. This behavior is seen, as this is parameter is tied to the time slice.

For a 15 minutes Backfill Slice, NetWall AVEVA Pi-Blue will go through all the points, and then go onto the next 15 minutes.

***For Example:***

Starting from 3:00-3:15, the Partial History Current Point parameter will go from 0 to total points, and then again when filling history for time slice 3:15-3:30 and so on.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

MetaDefender
