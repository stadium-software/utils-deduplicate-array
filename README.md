# Deduplicate List

A script to remove duplicates from any List

# Version 

1.0 Initial

# Global Script Setup
1. Create a Global Script called "DeduplicateList"
2. Add the input parameters below to the Global Script
   1. List
3. Add the output parameter below to the Global Script
   1. DeduplicatedList
4. Drag a *JavaScript* action into the script
5. Add the Javascript below into the JavaScript code property
```javascript
/* Stadium Script Version 1.0 https://github.com/stadium-software/utils-deduplicate-array */
let arr = ~.Parameters.Input.List;
const objectSorter = GFG_Object =>
    Object.keys(GFG_Object)  
        .sort()
        .reduce((finalObject, key) => {  
        finalObject[key] = GFG_Object[key];  
        return finalObject;  
    }, {}
); 
const uniqueArray = arr.filter((value, index) => {
    const _value = JSON.stringify(value);
    return index === arr.findIndex(obj => {
        return JSON.stringify(objectSorter(obj)) === _value;
    });
});
if (typeof arr[0] == "object") {
    return uniqueArray;
} else {
    return Array.from([...new Set(arr)]);
}
```
6. Drag a *SetValue* action into the Global Script and place it under the *JavaScript* action
   1. Target: = ~.Parameters.Output.DeduplicatedList
   2. Value: = ~.Javascript

![](images/Parameters.gif)

## Usage
1. Drag the script called "DeduplicateList" into a script or event handler
2. Pass a List into the scripts "List" input parameter
3. The script returns the a new list containing only unique values