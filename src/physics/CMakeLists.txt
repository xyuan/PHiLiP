SET(SOURCE
    physics_factory.cpp
    physics.cpp
    convection_diffusion.cpp
    burgers.cpp
    euler.cpp
    manufactured_solution.cpp
    mhd.cpp
    )

foreach(dim RANGE 1 3)
    # Output library
    string(CONCAT PhysicsLib Physics_${dim}D)
    add_library(${PhysicsLib} STATIC ${SOURCE})

    # Setup target with deal.II
    if(NOT DOC_ONLY)
        DEAL_II_SETUP_TARGET(${PhysicsLib})
    endif()

    target_compile_definitions(${PhysicsLib} PRIVATE PHILIP_DIM=${dim})

    # Setup target with deal.II
    unset(PhysicsLib)

endforeach()
