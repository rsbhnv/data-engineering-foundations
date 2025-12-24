# Execution Servers (Job Servers)

Execution Servers are responsible for running Talend Jobs.

## Characteristics
- Support parallel and distributed execution
- Enable workload balancing
- Improve performance and resiliency
- Can scale horizontally

## Execution Flow
- TAC triggers a Job execution
- Job Server retrieves the artifact from Nexus
- Job runs and reports status back to TAC
- Results and logs are persisted for monitoring

Virtual execution servers may be used to distribute load
and prevent system overload.
