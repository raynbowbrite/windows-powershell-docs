---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.ActiveDirectory.Management.dll-Help.xml
Module Name: ActiveDirectory
ms.date: 12/27/2016
online version: https://learn.microsoft.com/powershell/module/activedirectory/clear-adaccountexpiration?view=windowsserver2022-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: Clear-ADAccountExpiration
---

# Clear-ADAccountExpiration

## SYNOPSIS
Clears the expiration date for an Active Directory account.

## SYNTAX

```
Clear-ADAccountExpiration [-WhatIf] [-Confirm] [-AuthType <ADAuthType>] [-Credential <PSCredential>]
 [-Identity] <ADAccount> [-Partition <String>] [-PassThru] [-Server <String>] [<CommonParameters>]
```

## DESCRIPTION
The **Clear-ADAccountExpiration** cmdlet clears the expiration date for an Active Directory user or computer account.
When you clear the expiration date for an account, the account does not expire.

The *Identity* parameter specifies the user or computer account to modify.
You can identify a user or group by its distinguished name, GUID, security identifier (SID), or Security Accounts Manager (SAM) account name.
You can also set the *Identity* parameter to a user or computer object variable, such as `$<localUserObject>`, or pass a user or computer object through the pipeline to the *Identity* parameter.
For example, you can use the Get-ADUser, Get-ADComputer, or Search-ADAccount cmdlet to retrieve an object and then pass the object through the pipeline to the Clear-ADAccountExpiration cmdlet.

For Active Directory Lightweight Directory Services (AD LDS) environments, the *Partition* parameter must be specified except in the following two conditions:

- The cmdlet is run from an Active Directory provider drive.
- A default naming context or partition is defined for the AD LDS environment. 

To specify a default naming context for an AD LDS environment, set the **msDS-defaultNamingContext** property of the Active Directory directory service agent object (**nTDSDSA**) for the AD LDS instance.

## EXAMPLES

### Example 1: Clear an account expiration date for a specified user
```
PS C:\> Clear-ADAccountExpiration -Identity PattiFuller
```

This command clears the account expiration date for the user with SamAccountName PattiFuller.

### Example 2: Clear an account expiration date for a specified user using a distinguished name
```
PS C:\> Clear-ADAccountExpiration -Identity "CN=PattiFuller,DC=AppNC" -Server "PATTIFU-SVR1:60000"
```

This command clears the account expiration date for the user with DistinguishedName CN=PattiFuller,DC=AppNC on the AD LDS instance PATTIFU-SVR1:60000.

## PARAMETERS

### -AuthType
Specifies the authentication method to use.
The acceptable values for this parameter are:

- Negotiate or 0
- Basic or 1

The default authentication method is Negotiate.

A Secure Sockets Layer (SSL) connection is required for the Basic authentication method.

```yaml
Type: ADAuthType
Parameter Sets: (All)
Aliases: 
Accepted values: Negotiate, Basic

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm
Prompts you for confirmation before running the cmdlet.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential
Specifies the user account credentials to use to perform this task.
The default credentials are the credentials of the currently logged on user unless the cmdlet is run from an Active Directory module for Windows PowerShell provider drive.
If the cmdlet is run from such a provider drive, the account associated with the drive is the default.

To specify this parameter, you can type a user name, such as User1 or Domain01\User01 or you can specify a **PSCredential** object.
If you specify a user name for this parameter, the cmdlet prompts for a password.

You can also create a **PSCredential** object by using a script or by using the **Get-Credential** cmdlet.
You can then set the *Credential* parameter to the **PSCredential** object.

If the acting credentials do not have directory-level permission to perform the task, Active Directory module for Windows PowerShell returns a terminating error.

```yaml
Type: PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Identity
Specifies an Active Directory account object by providing one of the following property values.
The identifier in parentheses is the Lightweight Directory Access Protocol (LDAP) display name for the attribute.
The acceptable values for this parameter are:

- A distinguished name
- A GUID (objectGUID) 
- A security identifier (objectSid) 
- A SAM account name (sAMAccountName)

The cmdlet searches the default naming context or partition to find the object.
If two or more objects are found, the cmdlet returns a non-terminating error.

This parameter can also get this object through the pipeline or you can set this parameter to an account object instance.

Derived types such as the following are also accepted:

- **Microsoft.ActiveDirectory.Management.ADServiceAccount**
- **Microsoft.ActiveDirectory.Management.ADComputer**
- **Microsoft.ActiveDirectory.Management.ADUser**

```yaml
Type: ADAccount
Parameter Sets: (All)
Aliases: 

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Partition
Specifies the distinguished name of an Active Directory partition.
The distinguished name must be one of the naming contexts on the current directory server.
The cmdlet searches this partition to find the object defined by the *Identity* parameter.

In many cases, a default value is used for the *Partition* parameter if no value is specified. 
The rules for determining the default value are given below. 
Note that rules listed first are evaluated first and once a default value can be determined, no further rules are evaluated.

In Active Directory Domain Services (AD DS) environments, a default value for *Partition* is set in the following cases: 

- If the *Identity* parameter is set to a distinguished name, the default value of *Partition* is automatically generated from this distinguished name.
- If running cmdlets from an Active Directory provider drive, the default value of *Partition* is automatically generated from the current path in the drive. 
- If none of the previous cases apply, the default value of *Partition* is set to the default partition or naming context of the target domain.

In AD LDS environments, a default value for *Partition* is set in the following cases:

- If the *Identity* parameter is set to a distinguished name, the default value of *Partition* is automatically generated from this distinguished name. 
- If running cmdlets from an Active Directory provider drive, the default value of *Partition* is automatically generated from the current path in the drive. 
- If the target AD LDS instance has a default naming context, the default value of *Partition* is set to the default naming context. 
To specify a default naming context for an AD LDS environment, set the **msDS-defaultNamingContext** property of the Active Directory directory service agent (DSA) object (**nTDSDSA**) for the AD LDS instance. 
- If none of the previous cases apply, the *Partition* parameter will not take any default value.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru
Returns an object representing the item with which you are working.
By default, this cmdlet does not generate any output.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Server
Specifies the Active Directory Domain Services instance to connect to, by providing one of the following values for a corresponding domain name or directory server.
The service may be any of the following:  Active Directory Lightweight Domain Services, Active Directory Domain Services or Active Directory snapshot instance.

Specify the Active Directory Domain Services instance in one of the following ways:  

Domain name values:

- Fully qualified domain name
- NetBIOS name

Directory server values: 

- Fully qualified directory server name
- NetBIOS name
- Fully qualified directory server name and port

The default value for this parameter is determined by one of the following methods in the order that they are listed:

- By using the **Server** value from objects passed through the pipeline
- By using the server information associated with the Active Directory Domain Services Windows PowerShell provider drive, when the cmdlet runs in that drive
- By using the domain of the computer running Windows PowerShell

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf
Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### Microsoft.ActiveDirectory.Management.ADAccount
An account object (**Microsoft.ActiveDirectory.Management.ADAccount**) is received by the *Identity* parameter.

Derived types, such as the following are also accepted:

- **Microsoft.ActiveDirectory.Management.ADUser**
- **Microsoft.ActiveDirectory.Management.ADComputer**
- **Microsoft.ActiveDirectory.Management.ADServiceAccount**

## OUTPUTS

### None

## NOTES
* This cmdlet does not work with an Active Directory snapshot.
* This cmdlet does not work with a read-only domain controller.

## RELATED LINKS

[Search-ADAccount](./Search-ADAccount.md)

[Set-ADAccountExpiration](./Set-ADAccountExpiration.md)

[Get-ADUser](./Get-ADUser.md)

[Get-ADComputer](./Get-ADComputer.md)

[AD DS Administration Cmdlets in Windows PowerShell](./activedirectory.md)

