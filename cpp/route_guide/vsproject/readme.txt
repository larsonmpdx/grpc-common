visual studio configuration

I used msvc 2013 express

my grpc is installed in c:\local\grpc\

I generated the protobuf files using a linux install - I didn't want to try to get protoc into the build process

I used win32/debug for building grpc, protobuf, and route_guide.  I ran into trouble when compiling protobuf because I had an old vs project in the folder and I didn't notice git was skipping it when pulling (status can be hidden when it's a submodule).  A fresh pull with v3.0.0-alpha-3 worked fine.


visual studio project settings to change, if your grpc install is not in c:\local\:

additional include directories, under C++ options in each project file:
..\..\;C:\local\grpc\include;C:\local\grpc\third_party\protobuf\src

additional depdendencies, under linker options in each project file:
kernel32.lib;user32.lib;gdi32.lib;winspool.lib;comdlg32.lib;advapi32.lib;shell32.lib;ole32.lib;oleaut32.lib;uuid.lib;odbc32.lib;odbccp32.lib;gpr.lib;grpc.lib;grpc++.lib;libprotobuf.lib;ws2_32.lib;%(AdditionalDependencies)

not sure which of these libraries is actually needed, I just added everything.  ws2_32.lib is necessary for some windows socket things.

additional library directories, under linker options in each project file:
C:\local\grpc\vsprojects\Debug;C:\local\grpc\third_party\protobuf\vsprojects\Debug


