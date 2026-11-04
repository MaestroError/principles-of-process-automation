# Process Brief: Continuous condition maintenance

Kind: Prescriptive. A control unit maintains reservoir level within the approved operating band. The process owner is a supervisory system with authority to change the target within the approved envelope but not to change that envelope. The alert recipient is a separate supervisory controller with access to the reserve supply. No human role is assigned inside this boundary.

Readiness: valid level observations, available inflow/outflow control, and current operating permission. Continue while those conditions hold. Invalid level observations suspend ordinary regulation, initiate the approved maintained safe mode, and transfer sensor evidence, actions taken, and valve state to the alert recipient. The recipient must acknowledge within the approved control interval; otherwise remain in the maintained safe mode. A one-line 'do nothing' fallback is unacceptable because maintaining the safe mode consumes reserve supply and control capacity. Capacity exhaustion has an OPEN approved response owned by the governing authority; it blocks claiming the full exceptional path is ready.

Observe condition history and state transitions over daily intervals and compare drift weekly. This process has no scheduled finish and no newly produced artifact is required for success. Do not select a controller vendor or redesign the physical system.
