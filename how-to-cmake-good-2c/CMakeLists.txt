cmake_minimum_required(VERSION 3.12)
project(MyProject VERSION 1.1.2)

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