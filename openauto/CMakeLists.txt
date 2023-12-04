add_library(openauto SHARED
        App.cpp
        Service/BluetoothService.cpp
        Service/InputService.cpp
        Service/MediaAudioService.cpp
        Service/ServiceFactory.cpp
        Service/AudioInputService.cpp
        Service/SystemAudioService.cpp
        Service/AndroidAutoEntityFactory.cpp
        Service/AudioService.cpp
        Service/SensorService.cpp
        Service/SpeechAudioService.cpp
        Service/Pinger.cpp
        Service/AndroidAutoEntity.cpp
        Service/VideoService.cpp
        Service/NavigationStatusService.cpp
        Service/MediaStatusService.cpp
        Configuration/RecentAddressesList.cpp
        Configuration/Configuration.cpp
        Projection/RemoteBluetoothDevice.cpp
        Projection/OMXVideoOutput.cpp
        Projection/LocalBluetoothDevice.cpp
        Projection/VideoOutput.cpp
        Projection/InputDevice.cpp
        Projection/SequentialBuffer.cpp
        Projection/DummyBluetoothDevice.cpp
        Projection/QtVideoOutput.cpp
        Projection/GSTVideoOutput.cpp 
        Projection/QtAudioInput.cpp
        Projection/RtAudioOutput.cpp
        Projection/QtAudioOutput.cpp
        ${PROJECT_SOURCE_DIR}/btservice/AndroidBluetoothServer.cpp
        ${PROJECT_SOURCE_DIR}/btservice/AndroidBluetoothServer.cpp
        ${PROJECT_SOURCE_DIR}/btservice/AndroidBluetoothService.cpp
        ${PROJECT_SOURCE_DIR}/btservice/btservice.cpp
        ${PROJECT_SOURCE_DIR}/include/btservice/AndroidBluetoothServer.hpp
        ${PROJECT_SOURCE_DIR}/include/btservice/AndroidBluetoothService.hpp
        ${PROJECT_SOURCE_DIR}/include/btservice/IAndroidBluetoothServer.hpp
        ${PROJECT_SOURCE_DIR}/include/btservice/IAndroidBluetoothService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/App.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/Configuration.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/RecentAddressesList.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/AudioOutputBackendType.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/IConfiguration.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/IRecentAddressesList.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/HandednessOfTrafficType.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Configuration/BluetootAdapterType.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/NavigationStatusService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/MediaStatusService.hpp
	${PROJECT_SOURCE_DIR}/include/openauto/Service/MediaAudioService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/SensorService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IPinger.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IAndroidAutoEntity.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/SystemAudioService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IAndroidAutoEntityEventHandler.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/AudioInputService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/VideoService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IAndroidAutoEntityFactory.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/AudioService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IServiceFactory.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/BluetoothService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/AndroidAutoEntity.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/ServiceFactory.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/SpeechAudioService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/AndroidAutoEntityFactory.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/IService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/Pinger.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Service/InputService.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IInputDeviceEventHandler.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IVideoOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/RtAudioOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/LocalBluetoothDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IAudioOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/QtAudioInput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/VideoOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IBluetoothDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/OMXVideoOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IAudioInput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/DummyBluetoothDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/IInputDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/InputDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/QtAudioOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/RemoteBluetoothDevice.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/QtVideoOutput.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/SequentialBuffer.hpp
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/InputEvent.hpp
        )

if(GST_BUILD)
target_sources(openauto PRIVATE	
        ${PROJECT_SOURCE_DIR}/include/openauto/Projection/GSTVideoOutput.hpp
        )

target_include_directories(openauto SYSTEM PUBLIC
        ${QTGSTREAMER_INCLUDE_DIR}
        ${GST_INCLUDE_DIRS}
        )

target_link_libraries(openauto PRIVATE
        ${QTGSTREAMER_LIBRARY}
        ${GST_LIBRARIES}
        ${Qt5QuickWidgets_LIBRARIES}
        ${QTGSTREAMER_QUICK_LIBRARY}
        )
endif()

target_include_directories(openauto PRIVATE
        ${PROJECT_SOURCE_DIR}/include
        ${RTAUDIO_INCLUDE_DIRS}
        ${Protobuf_INCLUDE_DIRS}
        )

target_link_libraries(openauto PUBLIC
        libusb
        Threads::Threads
        ${Boost_LIBRARIES}
        aasdk
        h264
        rtaudio
        Qt5::Bluetooth
        Qt5::MultimediaWidgets
        btservice_proto
        ${Protobuf_LIBRARIES}
        )

install(TARGETS openauto
        LIBRARY DESTINATION lib)

set_target_properties(openauto
        PROPERTIES INSTALL_RPATH_USE_LINK_PATH 1)

install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/openauto DESTINATION include)
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/btservice DESTINATION include)
install(FILES ${PROJECT_SOURCE_DIR}/include/OpenautoLog.hpp DESTINATION include)
