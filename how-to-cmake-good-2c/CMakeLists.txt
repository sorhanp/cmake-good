cmake_minimum_required(VERSION 3.12)
project(MyProject VERSION 1.1.2)

### FUNCTIONS ###
function(cmake_function)
    message(STATUS "Function called!")
endfunction()

function(cmake_function_with_arg first_arg)
    message(STATUS "Function called with argument: ${first_arg}!")
endfunction()

function(cmake_function_arg_list first_arg)
    #Print only the non-named arguments so first_arg = 1, but ARGN-argument starts with #2
    foreach(arg IN LISTS ARGN)
        message(STATUS "ARGN-argument: ${arg}!")
    endforeach()

    #Print all the arguments
    foreach(arg IN LISTS ARGV)
        message(STATUS "ARGV-argument: ${arg}!")
    endforeach()
endfunction()

cmake_function()
cmake_function_with_arg(test)
cmake_function_arg_list(1 2 3 4 5 6 7 8)

### END OF FUNCTIONS ###


### SCOPE ###

#Function to display global variable scope with non-parent
function(cmake_scope_showcase_non_parent)
    message(STATUS "Value of global var is at non-parent function, before change: ${GLOBAL_VARIABLE_NONPARENT}!")

    set(GLOBAL_VARIABLE_NONPARENT Function)

    message(STATUS "Value of global var is at non-parent function, after change: ${GLOBAL_VARIABLE_NONPARENT}!")
endfunction()

#Function to display global variable scope with parent
function(cmake_scope_showcase_parent)
    message(STATUS "Value of global var is at parent function, before change: ${GLOBAL_VARIABLE_PARENT}!")

    set(GLOBAL_VARIABLE_PARENT Function PARENT_SCOPE)

    message(STATUS "Value of global var is at parent function, after change: ${GLOBAL_VARIABLE_PARENT}!")
endfunction()

## NONPARENT example
set(GLOBAL_VARIABLE_NONPARENT Global)
message(STATUS "Value of global non-parent var is before function call: ${GLOBAL_VARIABLE_NONPARENT}!")
cmake_scope_showcase_non_parent()
message(STATUS "Value of global non-parent var is after function call: ${GLOBAL_VARIABLE_NONPARENT}!")

message(STATUS "-----------------------------------------------------------")

## PARENT example
set(GLOBAL_VARIABLE_PARENT Global)
message(STATUS "Value of global parent var is before function call: ${GLOBAL_VARIABLE_PARENT}!")
cmake_scope_showcase_parent()
message(STATUS "Value of global parent var is after function call: ${GLOBAL_VARIABLE_PARENT}!")

### END OF SCOPE ###

## TODO Return VALUES