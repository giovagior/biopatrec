# Introduction #

The Virtual Reality Environment has been developed to provide an output for the BioPatRec. It visualises a hand on a black background, that can be moved using the predicted movement output from the BioPatRec.


# Details #

The Virtual Reality Environment (VRE) is written using Ogre3D, so when loading this you will see a configuration screen from Ogre3D where you can enter wanted resolution and other graphical features.

The VRE can be started but will not run until a Socket Connection is setup. During startup it listens to port **23068** for incoming connections on the local machine. Then a TCP connection is setup with the environment, where the data for movements is transferred according to the [VRE\_Protocol](VRE_Protocol.md).

A feature of the VRE is the [TACTest](TACTest.md). This is a test to see how fast a user can go to a desired position, for instance to close the hand, and will provide concrete data for direct comparison between pattern recognitions.

When using the VRE you cannot perform movements that are not supported. To see a list of the supported movements see the map of dofs in [VRE\_Protocol](VRE_Protocol.md) page.

# Execution #

The VRE is loaded when you wish to test the pattern recognition, usually from the [GUI\_TestPatRec](GUI_TestPatRec.md) routine, by pressing the appropriate button in the interface. This will load the configuration interface from Ogre3D, and it is important that this is not cancelled. If no socket connection is set up after the button is pressed **MATLAB may crash**.

_**Note:**_ To start the VRE, you must first disconnect the motor connection, and vice versa. If not correctly disconnected this may cause errors. Try disconnecting and re-connecting the acquisition card if any problems occur.

# Exiting #

When exiting the VRE, either by disconnecting the connectiong from MATLAB or closing the window, you may get an error message that reads: _This application has requested the Runtime to terminate it in an unusual way. Please contact the application's support team for more information._
This error occurs often when closing. This is a known error, and does not affect the performance of the program. It has been added to the ToDo for the next release.