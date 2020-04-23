# UNIFIED LOGGING

Define **subsystems** to organize large topics of app. E.g., one subsystem per process. Within subsystem, define **categories** to further distinguish parts. E.g., model code, UI code. In game: physics, AI, world sim, rendering.

To record data, log message to particular subsystem and category. Each message also has log level, which describes type of info. E.g., error message indicates significant error, so logging system always logs to persistent store. More verbose debug message on inner workings; recorded only when requested.

Can group messages with **activity**. Activity is request made to or by subsystem, usually triggered by user action. E.g., when user selects menu item, app performs sequence of related actions. May log messages across different subsystems or categories, but correlated by same activity for context. Another example activity is database update.

To visualize performance data in Instruments, use same subsystems to record **signposts**. Signposts represent critical one-time events or start and end times of interval. E.g., when processing data, capture start and end times for calculation. In Instruments, see info visually and track events over time. Can create custom instruments to automatically analyze data.
