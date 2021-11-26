# Profile Version

Starts from Surge iOS 4.9.3 & Surge Mac 4.2.2. The profile now supports version remark for better backward compatibility.

For example:
```
[Script]
panel = script-path=panel.js,type=generic 
```

The old versions of Surge don't support the generic type script declaration. Then this line would occur a profile parsing error.

```
[Script]
#!PROFILE-VERSION-REQUIRED 10 panel = script-path=panel.js,type=generic 
```

By adding a profile version requirement prefix, the old versions will treat the line as a comment and ignore it.

*Please notice that the feature is for profile distribution, such as managed profile and enterprise profile. When the profile is modified by UI all the version remarks will be removed.*

## Profile Version Change Notes

### Version 0 (All versions below Surge iOS 4.9.3 & Surge Mac 4.2.2)

### Version 10 (Starts from Surge iOS 4.9.3 & Surge Mac 4.2.2)

- Supports script type 'generic'.
- Supports new section [Panel]. (This doesn't require a profile version requirement since an unknown section won't be parsed.)

