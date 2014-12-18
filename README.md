General usage is simple: `include "autoinit_funcs.h"`, declare or define two
functions with zero parameters (void) and any return type: one for
initialization and one for deinitialization, add 
`_SET_INIT_AND_DEINIT_FUNCS(FuncInitName, FuncDeInitName)` to the code
and functions will be automatically called during application startup
and shutdown.

This is useful for libraries as libraries doesn't have direct access
to `main()` functions.

Example:

```` C
#include <stdlib.h>
#include "autoinit_funcs.h"

int someVar;
void* somePtr;

void libInit(void)
{
  someVar = 3;
  somePtr = malloc(100);
}

void libDeinit(void)
{
  free(somePtr);
}

_SET_INIT_AND_DEINIT_FUNCS(libInit,libDeinit);
````

If initializer or deinitializer functions is not needed, just define
it as empty function.

This header should work with GCC, clang, MSVC (2010 or later).
Supported C and C++ languages; application, static and dynamic (DLL)
libraries; non-optimized (Debug) and optimized (Release) compilation
and linking.

For more information see header code and comments in code.
