# Distributed under the OSI-approved BSD 3-Clause License.  See accompanying
# file LICENCE.txt or https://cmake.org/licensing for details.

enable_language(OBJC)

set(ExampleApp_SOURCES
    AAPLAppDelegate.m
    AAPLRenderer.m
    AAPLViewController.m
    main.m
)

set(ExampleApp_HEADERS
    AAPLAppDelegate.h
    AAPLRenderer.h
    AAPLViewController.h
)

set(ExampleApp_RESOURCES
    Main.storyboard
)

add_executable(ExampleApp MACOSX_BUNDLE
    ${ExampleApp_SOURCES} ${ExampleApp_HEADERS} ${ExampleApp_RESOURCES}
)
add_dependencies(ExampleApp ShaderBase)

set_target_properties(ExampleApp PROPERTIES
    MACOSX_BUNDLE_INFO_PLIST "${CMAKE_CURRENT_SOURCE_DIR}/Info.plist"
    RESOURCE "${ExampleApp_RESOURCES}"
    XCODE_EMBED_RESOURCES ShaderBase
)

target_link_libraries(ExampleApp
    PRIVATE
    "-framework Cocoa"
    "-framework Metal"
)

target_include_directories(ExampleApp
    PRIVATE
    ../ShaderBase
)