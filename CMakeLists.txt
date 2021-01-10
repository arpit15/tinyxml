# tinyxml file
# Note that we use this since urdfdom (ROS) uses this too
# Files come from: http://sourceforge.net/projects/tinyxml/

 cmake_minimum_required( VERSION 2.8 )
project(tinyxml)

################################
# Add common source 

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/.")

add_definitions(-DTIXML_USE_STL)

set( tinyxml_srcs tinyxml.cpp tinyxmlparser.cpp tinyxmlerror.cpp tinystr.cpp )
set( tinyxml_hdrs tinyxml.h tinystr.h )
################################
# Add targets
set(BUILD_STATIC_LIBS OFF CACHE BOOL "Set to ON to build static libraries")
if(BUILD_STATIC_LIBS)
	add_library(tinyxmlstatic STATIC ${tinyxml_srcs} ${tinyxml_hdrs} )
	set_target_properties(tinyxmlstatic PROPERTIES OUTPUT_NAME tinyxml)
endif(BUILD_STATIC_LIBS)

add_library( TinyXML SHARED ${tinyxml_srcs} ${tinyxml_hdrs} )
#set_target_properties( TinyXML tinyxmlstatic PROPERTIES FOLDER ThirdParty/tinyxml )
set_target_properties(TinyXML PROPERTIES PUBLIC_HEADER "tinyxml.h;tinystr.h")

install( TARGETS TinyXML EXPORT tinyxmlTargets )
#install( FILES ${tinyxml_hdrs} DESTINATION include )

install(EXPORT tinyxmlTargets
 FILE TinyXml.cmake
  NAMESPACE TinyXml::
  DESTINATION lib/cmake/TinyXml
 )
