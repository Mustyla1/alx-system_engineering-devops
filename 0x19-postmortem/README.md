Issue Summary

Duration: March 12, 2025, 03:15 WAT – March 12, 2025, 05:45 WAT (2 hours, 30 minutes)

Impact:

80% of users were unable to access our web application.

API requests resulted in 503 Service Unavailable errors.

Website response time increased from 200ms to over 10s for the remaining 20% of users.

Root Cause: A memory leak in the backend service caused excessive resource consumption, leading to server crashes and unresponsiveness.

Timeline

03:15 WAT - Monitoring alerts triggered high response times and increased error rates.

03:20 WAT - Engineers started investigating, assuming a database issue due to slow queries.

03:40 WAT - Attempted database scaling but observed no improvement.

04:00 WAT - Issue escalated to the backend team after ruling out database concerns.

04:15 WAT - Logs reviewed, revealing excessive memory consumption by the authentication service.

04:30 WAT - Restarted authentication service, providing temporary relief.

04:45 WAT - Further investigation identified a recent code deployment as the culprit.

05:00 WAT - Rolled back to a previous stable version.

05:30 WAT - Performance normalized, and services were fully restored.

05:45 WAT - Incident declared resolved.

Root Cause and Resolution

The memory leak was traced to a recent update in the authentication service, which improperly handled session caching.

Every authentication request increased memory allocation without proper garbage collection, causing memory exhaustion.

Restarting the service provided temporary relief but did not resolve the underlying problem.

A rollback to the last stable version stopped memory leaks and restored normal operations.

Post-mortem debugging revealed that the caching mechanism in the update had an infinite retention period for session tokens.

Corrective and Preventative Measures

Improvements

Implement memory usage monitoring for backend services.

Enhance load testing before rolling out new deployments.

Improve alerting to detect abnormal memory growth.

TODO List:



This incident highlighted the importance of comprehensive testing and proactive monitoring. By implementing these corrective actions, we aim to prevent similar outages in the future.
