#
# Tests configuration
#

include_directories($<TARGET_PROPERTY:EnTT,INTERFACE_INCLUDE_DIRECTORIES>)
add_compile_options($<TARGET_PROPERTY:EnTT,INTERFACE_COMPILE_OPTIONS>)

add_executable(helper entt/entity/helper.cpp)
set_target_properties(helper PROPERTIES CXX_EXTENSIONS OFF)
target_link_libraries(helper PRIVATE EnTT GTest::Main Threads::Threads)
target_compile_definitions(helper PRIVATE $<TARGET_PROPERTY:EnTT,INTERFACE_COMPILE_DEFINITIONS>)
target_compile_features(helper PRIVATE $<TARGET_PROPERTY:EnTT,INTERFACE_COMPILE_FEATURES>)
target_compile_options(helper PRIVATE $<$<NOT:$<CXX_COMPILER_ID:MSVC>>:-pedantic -Wall>)
target_compile_options(helper PRIVATE $<$<CXX_COMPILER_ID:MSVC>:/EHsc>)
add_test(NAME helper COMMAND helper)
