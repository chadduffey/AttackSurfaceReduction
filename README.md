# Windows Attack Surface Reduction rules
You can read more about ASR [here](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction). This script will help to quickly configure ASR rules on non domain joined machines. Just use `configure.ps1`

For each protection offered by ASR, just choose whether you'd like:
- Audit mode (uncomment the first line)
- Enforced mode (uncomment the second line)
- Nothing (leave it alone)

## Example

I want to enforce "Block Adobe Reader from creating child processes":

```
#Block Adobe Reader from creating child processes
#Add-MpPreference -AttackSurfaceReductionRules_Ids 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c -AttackSurfaceReductionRules_Actions AuditMode
Set-MpPreference -AttackSurfaceReductionRules_Ids 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c -AttackSurfaceReductionRules_Actions Enabled
```

But i just want to audit "Block executable files from running unless they meet a prevalence, age, or trusted list criterion":

```
#Block executable files from running unless they meet a prevalence, age, or trusted list criterion
Add-MpPreference -AttackSurfaceReductionRules_Ids 01443614-cd74-433a-b99e-2ecdc07bfc25 -AttackSurfaceReductionRules_Actions AuditMode
#Set-MpPreference -AttackSurfaceReductionRules_Ids 01443614-cd74-433a-b99e-2ecdc07bfc25 -AttackSurfaceReductionRules_Actions Enabled
```

## To Remove Rules

```
Add-MpPreference -AttackSurfaceReductionRules_Ids <rule ID> -AttackSurfaceReductionRules_Actions Disabled
```
Or `delete.ps1` is there to make this faster if needed; just comment out what you'd like to leave alone.
