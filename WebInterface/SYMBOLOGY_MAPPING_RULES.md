# Symbology Mapping Rules

**⚠️ CRITICAL: Always maintain consistency with Android EBarcodesSymbologies enum**

## Rule #1: Single Source of Truth
The Android enum `EBarcodesSymbologies.java` is the **SINGLE SOURCE OF TRUTH** for all symbology mappings.

**Location**: `AI_MultiBarcodes_Capture/src/main/java/com/zebra/ai_multibarcodes_capture/helpers/EBarcodesSymbologies.java`

## Rule #2: Mandatory Mapping File Usage
ALL symbology-related code MUST use the centralized mapping file:
- **File**: `WebInterface/src/api/symbology-mapping.php`
- **Class**: `SymbologyMapping`

## Rule #3: Never Hardcode Symbology Maps
**NEVER** hardcode symbology mappings directly in:
- PHP API files
- JavaScript files
- Database procedures
- Any other code files

## Rule #4: Verification Process
When making ANY changes to symbology handling:

1. **Check Android enum** for the correct integer values
2. **Update mapping file** if needed: `symbology-mapping.php`
3. **Test mapping** with actual barcode data
4. **Verify consistency** across all components

## Rule #5: Display Names
- Use the **exact display names** from the Android enum
- **Remove underscores** for UI display (e.g., `EAN_13` → `EAN 13`)
- **Keep integer values** exactly as defined in Android enum

## Examples of Correct Mapping
```
Integer Value → Android Enum → Display Name
0 → EAN_8 → "EAN 8"
1 → EAN_13 → "EAN 13"
26 → AUSTRALIAN_POSTAL → "AUSTRALIAN POSTAL"
```

## Common Mistakes to Avoid
❌ **WRONG**: Hardcoding mappings in barcodes.php
❌ **WRONG**: Using different integer values than Android enum
❌ **WRONG**: Displaying enum names with underscores in UI
❌ **WRONG**: Creating separate mapping files for different components

✅ **CORRECT**: Using `SymbologyMapping::getSymbologyName($id)`
✅ **CORRECT**: Integer values match Android enum exactly
✅ **CORRECT**: Clean display names without underscores
✅ **CORRECT**: Single centralized mapping file

## Implementation Checklist
- [ ] Android enum is the authoritative source
- [ ] All code uses `SymbologyMapping` class
- [ ] No hardcoded mappings exist
- [ ] Display names are clean (no underscores)
- [ ] Integer values match Android enum
- [ ] Tests verify mapping consistency

## Enforcement
This rule MUST be enforced in:
- Code reviews
- Pull request checks
- Integration tests
- Documentation updates

**Breaking this rule will cause data inconsistency and incorrect barcode symbology display.**