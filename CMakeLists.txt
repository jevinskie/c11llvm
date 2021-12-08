add_library(CDSPass MODULE
    # List your source files here.
    CDSPass.cpp
)

# Use C++11 to compile our pass (i.e., supply -std=c++11).
set_property(TARGET CDSPass PROPERTY CXX_STANDARD 20)

# LLVM is (typically) built with no C++ RTTI. We need to match that.
set_target_properties(CDSPass PROPERTIES
    COMPILE_FLAGS "-fno-rtti"
)

# Get proper shared-library behavior (where symbols are not necessarily
# resolved when the shared library is linked) on OS X.
if(APPLE)
    set_target_properties(CDSPass PROPERTIES
        LINK_FLAGS "-undefined dynamic_lookup"
    )
endif(APPLE)