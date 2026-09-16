<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/schedule-report -->

# Schedule Report

The scheduled report will generate and deliver periodic updates tailored for the administrator. These reports are designed to provide comprehensive insights and relevant data, enabling informed decision-making and efficient management of ongoing tasks or operations.

## [Processing Activity](/docs/mdcore/v5.22.0/configuration/schedule-report#processing-activity)

The system generates a detailed report in CSV format, for file processing activities, offering comprehensive insights similar to the processing history. However, these reports are scheduled to be produced periodically and delivered automatically, ensuring consistent and timely updates without manual intervention.

- **Result**: Allows users to specify a predefined outcome to filter data when generating reports for processing activities. This ensures that only relevant information is included in the report.
- **Report Time Range**: Defines the specific time period for which the report will collect data. This helps in focusing on activities within a particular timeframe.
- **Schedule Time**: Configures the periodic schedule for sending reports. The following options are available for selection:

  - Daily
  - Weekly
  - Monthly
  - Quarterly
  - Onetime - send the report only one time

## [Executive Report](/docs/mdcore/v5.22.0/configuration/schedule-report#executive-report)

The system offers the ability to generate scheduled reports in PDF format, similar to the "Executive Report" available under the Dashboard. These reports are designed to provide a concise and professional summary of key metrics and insights, delivered automatically at predefined intervals.

- **Report type**: Enables users to select the type of report they want to generate. Options include filtering by `Workflow` , by `Users` , by `Sources` , or a combination of both `Users and Sources` .
- **Workflow:** Allows users to specify a particular workflow rule to focus the report on relevant processing activities.
- **Result Type**: Object or File
- **Report Time Range**: Defines the specific time period for which the report will collect data.
- **Schedule Time**: Configures the periodic schedule for sending reports. The following options are available for selection:

  - Daily
  - Weekly
  - Monthly
  - Quarterly
  - Onetime - send the report only one time
