# target: storage_charge_test
file(GLOB all_tests CONFIGURE_DEPENDS
  *.cc
  *.c
)

add_executable(storage_charge_test ${all_tests})

target_link_libraries(storage_charge_test 
  PRIVATE
    storage_charge 
    GTest::gtest 
    GTest::gtest_main
)

add_test(NAME storage_charge_test COMMAND storage_charge_test)