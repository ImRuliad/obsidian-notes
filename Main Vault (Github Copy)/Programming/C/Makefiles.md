# What does a makefile do?
- The things to build (*targets*)
- The steps identified to build them
- The dependencies required

*This allows us to make sure all file changes are updated and included in an automated fashion in larger programs*
*Make keeps track of dependencies, what needs recompiling, and what needs relinking.*

- ### Makefiles *targets* identify *tasks*
- ### *Dependencies* are identified after the *targets*
- ### *Recipe* or *action lines* identify what to do
- ### *Action lines* must start with a tab character
- ### *Rules* include the *Target*, the *Dependencies*, and a *recipe*
- ### The default *Target* is the first *Target* listed in the makefile.


--- start-multi-column: ExampleRegion2  
```column-settings  
number of columns: 2
Column Spacing: 10px
```
## *A Simple Makefile*
![[Screenshot 2024-10-29 at 6.14.25 PM.png|400]]


--- end-column ---

## *A Complex Makefile*
![[Screenshot 2024-10-29 at 6.26.38 PM.png|400]]


--- end-multi-column


# Makefile Macros
- #### Makefiles have *built-in* macros (already included)
- #### Makefiles also have *user defined* macros (we have to define them)
### Built-in Macros:
- *CC* - Program for compiling C programs.
- *RM* - Command to remove a file (defaults to rm -f)
### User Defined Macros
- *Usually defined at the top of the makefile.*
-  *INCFLG = -I ./utils* - Defining INCFLG as a variable to hold a macro. *-I* is a compiler flag to specify an include path for *header files*. *./utils* is where the compiler will look for these header files.
