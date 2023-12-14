SLF4J Logging levels are listed below by order of severity/urgency.
1. TRACE
2. DEGUB
3. INFO
4. WARN
5. ERROR
Setting the logging level at a particular level will report logs for that level and all levels above it.

# TRACE
Use this logging level to log all information that helps us to trace the processing of an incoming request though our application.

Examples for using TRACE level are:
* Start or end of a method, possibly including the processing duration.
* URLs of the endpoints of our application that have been called.
* Start and end of the processing of an incoming request or scheduled job.
# DEBUG
Use this logging level to log any information that helps us identify what went wrong.

Examples for using the DEGUB level are:
* Error messages when an incoming HTTP request was malformed, resulting in a 4xx HTTP status
* Variable value in business logic.

The DEBUG level may be used more generously than the other levels, but the code should not be littered with DEBUG statements as it reduces readability and pollutes the log.

# INFO
Use this logging level to document state changes in the application or some entity within the application. This information can be useful during development and sometimes even in production to track what is actually happening in the system.

Examples for using the INFO level are:
* The application has started with configuration parameter x having the value y.
* A new entity has be created or changed its state.
* The state of a certain process has changed from "open" to "processed".
* A regularly scheduled batch job has finished and processed z items.

# WARN
Use this logging level when something bad happened, but the application still has the chance to heal itself or the issue can wait a day or two to be fixed.

WARN events should be attended, so there must be some kind of alerting in place for the production environment.

A concrete example for a WARN message is when a system failed to connect to an external service, but will try again automatically. It might ultimately result in an ERROR log message when the retry-mechanism also fails.

**The WARN level is the level that should be active in production systems by default, so that only WARN and ERROR messages are being reported. This will save storage capacity and performance.**

If storage and performance are not an problem and the log server provides good search capabilities we can actually report even INFO and DEGUB events and just filter them out when we're only interested in the important stuff.

# ERROR
Use this logging level when the application is in trouble. Users are being affected without having a way to work around the issue. 

There must be some kind of alerting in place for ERROR log events in the production environment so that someone can fix the issue immediately.


Don't overuse this logging level because that would add too much noise to the logs and reduce the significance of a single ERRROR event. Often, the only use for the ERROR level within an application is when a valuable business use case cannot be completed due to technical issues or a bug.

# Conclusion
**There must be some kind of alerting on the WARN and ERROR levels and someone responsible to act on it for production and pre-production environments.**
