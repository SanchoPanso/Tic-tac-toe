cmake_minimum_required (VERSION 2.4)
project (tic-tac-toe)

find_package (PkgConfig REQUIRED)
pkg_check_modules (GTK2 REQUIRED gtk+-3.0)

include_directories (${GTK2_INCLUDE_DIRS})
link_directories (${GTK2_LIBRARY_DIRS})

add_library(game_logic game_logic.c)
add_library(bot bot.c)
add_library(gui gui.c)
add_library(cli cli.c)


add_executable(tic_tac_toe main.c)

add_definitions (${GTK2_CFLAGS_OTHER})
target_link_libraries (tic_tac_toe ${GTK2_LIBRARIES})
target_link_libraries (gui ${GTK2_LIBRARIES})


target_link_libraries(bot game_logic)

target_link_libraries(gui game_logic)
target_link_libraries(gui bot)

target_link_libraries(cli game_logic)
target_link_libraries(cli bot)

target_link_libraries(tic_tac_toe gui)
target_link_libraries(tic_tac_toe cli)

# PUBLIC