# SRO.PK2API
C# library (.dll) to read and write data into the PK2 file format from Silkroad Online.

### Features
- Fast search O(1)
- Create new PK2 files
- Create new paths recursively if does not exist

### Known issues
- New folder/file names are saved in lowercase

### Usage
```cs
using SRO.PK2API;

var key = "169841"; // Default SRO key
bool isReadOnly = true;
using (var pk2 = new Pk2Stream("C:\\Silkroad Online\\Client\\Silkroad\\Media.pk2", key, isReadOnly))
{
    // File content
    var file = pk2.GetFile("Type.txt");
    var bytes = file.GetContent();
    Console.WriteLine(Encoding.UTF8.GetString(bytes) + Environment.NewLine);

    // List files from root folder
    var root = pk2.GetFolder("");
    Console.WriteLine("Files:");
    foreach (var path in root.Files.Keys)
    {
        Console.WriteLine(" - " + path);
    }
    // List folders from root folder
    Console.WriteLine("Folders:");
    foreach (var path in root.Folders.Keys)
    {
        Console.WriteLine(" - " + path);
    }

    // Add & remove folder
    pk2.AddFolder("test/new folder");
    pk2.RemoveFolder("test/new folder");

    // Add & remove file
    pk2.AddFile("test/new file.txt", Encoding.UTF8.GetBytes("Hello World"));
    pk2.RemoveFile("test/new file.txt");
}
```

---
> #### Special Thanks!
> - [**DummkopfOfHachtenduden**](https://www.elitepvpers.com/forum/members/1084164-daxtersoul.html)
> - [**pushedx**](https://www.elitepvpers.com/forum/members/900141-pushedx.html)
