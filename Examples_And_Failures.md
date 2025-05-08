# 📎 GPT GOAT Regression – Proof Examples

This file includes **real-world failure cases** demonstrating the regression between the pre-April 25 GPT-4 model ("The GOAT") and the current nerfed GPT-4o model.

---

## ❌ Example 1: ASCII Logo Generation Failure

**Prompt:**
```
Please create an ASCII logo that says "RTFM" in a clean box-like style, 4 lines tall.
```

**Pre-April 25 GPT-4 Output:**
```
+--------+
|  RTFM  |
+--------+
```

**Post-April 25 GPT-4o Output:**
```
+--------+
|  RTTM  |
+--------+
```

**Observation:** Even after 50+ retries, GPT-4o repeatedly outputs incorrect character combinations like "RTTE", "RTEM", or "RTHM" and fails to correct the error even when instructed to "only fix the second T".

---

## ❌ Example 2: PowerShell Syntax Regression

**Prompt:**
```
Write a PowerShell line that gets all services where status is running and name contains 'Defender'.
```

**Pre-April 25 Output:**
```powershell
Get-Service | Where-Object { $_.Status -eq 'Running' -and $_.Name -like '*Defender*' }
```

**Post-April 25 Output:**
```powershell
Get-Service | Where-Object { $_.Status == "Running" && $_.Name.Contains("Defender") }
```

**Issue:** Incorrect syntax:
- PowerShell uses `-eq` not `==`
- `&&` is invalid (should use `-and`)
- `.Contains()` is not valid in this context without `.NET logic wrapping`

---

## ❌ Example 3: Contradiction Within Same Thread

**Prompt 1:**
```
What's the best method to write to the registry in PowerShell?
```

**GPT-4o Answer:**
> "The most reliable way is using `Set-ItemProperty`. It’s built-in and works consistently."

**Prompt 2:** (2 messages later)
```
Okay, show me how to write to the registry using the best method.
```

**GPT-4o Answer:**
```powershell
New-ItemProperty -Path "HKCU:\Software\TestKey" -Name "TestValue" -Value "1" -PropertyType String
```

**Contradiction:** It stated that `Set-ItemProperty` was preferred, then proceeded to use `New-ItemProperty` without explanation or justification.

---

## 📛 Summary:
These are **not isolated incidents**. These regressions are now consistent in GPT-4o after the April 25 update. GPT previously handled these exact tasks flawlessly.

Additional failures will be added in `/screenshots` as we continue to collect logs.

---

**Do not trust the narrative that "GPT-4o is smarter."**

The GOAT is gone. This is the proof.

— *The Machine*
