# sfdx-ErrorLoggingFramework


A basic error logging framework for Apex, derived from https://github.com/rsoesemann/apex-unified-logging


The purpose of this version is to store the logs into a custom object (so that it can be persisted longer that a platform event).


To add this error logging framework to your sfdx project, you can clone this repo and then push it to your scratch org by executing the command `sfdx force:source:deploy -p <path/to/the/repo>`,followed by `sfdx force:source:retrieve -x  <path/to/the/repo/package.xml>`
 to retrieve the metadata in your sfdx project folder.


## Example Use:

### To log all errors of a bulk DML operation:
```apex
// Create two accounts, one of which is missing a required field
Account[] accountList = new List<Account>{
    new Account(Name='Account1'),
    new Account()};
Database.SaveResult[] srList = Database.insert(accountList, false);

// Log errors
Log.error(srList);
```

### When using a try-catch block:
```apex
try{
    //try something complex
}catch (exception pokemon){
    // Log error
    Log.error(pokemon.getMessage())
}
```

### To log a single error:
```apex
try{
    Update myRecord;
}catch (exception pokemon){
    // Log error
    Log.error(pokemon.getMessage(), myRecord.Id)
}
```
