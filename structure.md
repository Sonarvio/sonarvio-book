# Structure

After the initial idea following steps got defined:

1.  getting source data
2.  apply transforms for comparison
3.  use a service to look up hashed in a database
4.  find shops offering the song

From the beginning it was clear that aside of a shared persistent web application, a user specific browser extension would be required for the input. Although the hosted application would allow to manually select existing files to be analyzed, accessing data of 3rd a party websites still wouldn't be possible.

Since at the time each of the major browser vendors have their own extension scheme - the idea was to just write a minimum of platform specific code and focus on share-able elements. Furthermore one the core components, a visual editor to specify the sequence to be analyzed, should be re-usable by the extension and the web application. Both will also communicate with a server which handles the access to other APIs and deals with persistent data.

![Architecture Overview](Architecture-Overview.png)