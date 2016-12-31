https://msdn.microsoft.com/en-us/windows/uwp/files/quickstart-reading-and-writing-files

<!-- MDTOC maxdepth:6 firsth1:1 numbering:0 flatten:0 bullets:1 updateOnSave:1 -->

- [Create File](#create-file)   
- [Writing text to a File](#writing-text-to-a-file)   
- [Write bytes to a File by using a buffer](#write-bytes-to-a-file-by-using-a-buffer)   
- [Write text to a file by using a stream](#write-text-to-a-file-by-using-a-stream)   

<!-- /MDTOC -->
# Create File
```cs
Windows.Storage.StorageFolder storageFolder =
    Windows.Storage.ApplicationData.Current.LocalFolder;

Windows.Storage.StorageFile sampleFile =
    await storageFolder.CreateFileAsync("sample.txt",
        Windows.Storage.CreationCollisionOption.ReplaceExisting);
```
# Writing text to a File
__1. Locate Folder__
```cs
Windows.Storage.StorageFolder storageFolder =
    Windows.Storage.ApplicationData.Current.LocalFolder;
```
__2. Open File__
```cs
Windows.Storage.StorageFile sampleFile =
    await storageFolder.GetFileAsync("sample.txt");
```
__3. Write__
```cs
await Windows.Storage.FileIO.WriteTextAsync(sampleFile, "Swift as a shadow");
```

# Write bytes to a File by using a buffer
__0. Open File__
```cs
Windows.Storage.StorageFile sampleFile =
    await storageFolder.GetFileAsync("sample.txt");
```
__1. `ConvertStringToBinary`__
First, call `ConvertStringToBinary` to get a buffer of the bytes (based on an arbitrary string) that you want to write to your file.

```cs
var buffer = Windows.Security.Cryptography.CryptographicBuffer.ConvertStringToBinary(
        "What fools these mortals be",
        Windows.Security.Cryptography.BinaryStringEncoding.Utf8);
```
__2. Write__
Then write the bytes from your buffer to your file by calling the `WriteBufferAsync` method of the `FileIO` class.
```cs
await Windows.Storage.FileIO.WriteBufferAsync(sampleFile, buffer);
```

# Write text to a file by using a stream
__1. Open File__
```cs
Windows.Storage.StorageFile sampleFile =
    await storageFolder.GetFileAsync("sample.txt");
```

__2. OpenAsync, Get Stream__
Open the file by calling the `StorageFile.OpenAsync` method. It returns a stream of the file's content when the open operation completes.
```cs
var stream = await sampleFile.OpenAsync(Windows.Storage.FileAccessMode.ReadWrite);
```
__3. Get _output stream_ from _stream___
Get an output stream by calling the `GetOutputStreamAt` method from the stream. Put this in a `using` statement to manage the output stream's lifetime.

```cs
using (var outputStream = stream.GetOutputStreamAt(0))
{
    // We'll add more code here in the next step.
}
stream.Dispose(); // Or use the stream variable (see previous code snippet) with a using statement as well.
```

__4. Write__
Now add this code within the existing `using` statement to write to the output stream by creating a new `DataWriter` object and calling the `DataWriter.WriteString` method.
```cs
using (var outputStream = stream.GetOutputStreamAt(0))
{
    // We'll add more code here in the next step.
    using (var dataWriter =
            new Windows.Storage.Streams.DataWriter(outputStream))
    {
    dataWriter.WriteString("DataWriter has methods to write to various types, such as DataTimeOffset.");
    }
}
stream.Dispose(); // Or use the stream variable (see previous code snippet) with a using statement as well.

```
