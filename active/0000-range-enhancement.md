- Start Date: 2015-01-15
- RFC PR: (leave this empty)
- Revel Issue: (leave this empty)

# Summary

Enhance range validation to include float and int ranges, also limit fractional digits will be an option

# Motivation

Current range validation only works on integers, this will expand revels built in capabilities to validate floats as well.

# Detailed design

The current `range` validator along with `min` and `max` validators only work with integers. This proposal is to change this suite of validators to be floats instead. Integer validation will still be available using the float validator with 0 fractional units. Adding new function names is required to provide unique signatures for the methods to distinguish them from the 
integer only couter-parts. Structures will be changed to accept floats for comparisons and a new field for limiting the fractional units.

    type Min struct {
    	Min int
    	FractionalLimit int
    }
    
    type Max struct {
    	Max int
    	FractionalLimit int
    }
    
Existing functions:

    ValidMin
    ValidMax
    ValidRange
    
New functions added:

    ValidMinFloat
    ValidMaxFloat
    ValidRangeFloat
    
Existing functions will call the Float version with a 0 fractional unit, for example `ValidMax` would call `ValidMaxFloat` with a 0 fractional unit like below

    func ValidMax(max int) MaxSize {
        return ValidMaxFloat(max, 0);
    } 
    func ValidMaxFloatSize(max float64, fractional int) MaxSize {
        return Max{max, fractional};
    } 
    


# Drawbacks

Adds more code to the code base, by adding this the project gets bigger and more complex

Changing Max, Min structures may cause incompatible issues if people used these structures directly

# Alternatives

Alternatively we let the people implement there own validation

# Unresolved questions
Question
Should we add new functions like ValidMaxFloatSize, or should we just allow someone to pass in one or more arguments and decide programmatically what route to take? 

Answer
We loose runtime checking if we do things programmatically. 
(Most people seem to be against doing it programmatically)

Question
Should we modify the internal structures of Max, Min to be a float value ?

Impact in theory should be minimal if we change these, mostly these instances were used internally by the validator, but there may be cases of people using them directly

Answer

Question
What should the float function signatures look like ?

Answer



 
