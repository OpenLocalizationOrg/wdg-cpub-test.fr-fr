# Enumerate and query files and folders


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]


Access files and folders in either a folder, library, device, or network location. You can also query the files and folders in a location by constructing file and folder queries.

**Note**  Also see the [Folder enumeration sample](http://go.microsoft.com/fwlink/p/?linkid=619993).

 
## Prerequisites

-   **Understand async programming for Universal Windows Platform (UWP) apps**

    You can learn how to write asynchronous apps in C\# or Visual Basic, see [Call asynchronous APIs in C\# or Visual Basic](https://msdn.microsoft.com/library/windows/apps/mt187337). To learn how to write asynchronous apps in C++, see [Asynchronous programming in C++](https://msdn.microsoft.com/library/windows/apps/mt187334).

-   **Access permissions to the location**

    For example, the code in these examples require the **picturesLibrary** capability, but your location may require a different capability or no capability at all. To learn more, see [File access permissions](file-access-permissions.md).

## Enumerate files and folders in a location

**Note**  Remember to declare the **picturesLibrary** capability.

In this example we first use the [**StorageFolder.GetFilesAsync**](https://msdn.microsoft.com/library/windows/apps/br227276) method to get all the files in the root folder of the [**PicturesLibrary**](https://msdn.microsoft.com/library/windows/apps/br227156) (not in subfolders) and list the name of each file. Next, we use the [**GetFoldersAsync**](https://msdn.microsoft.com/library/windows/apps/br227280) method to get all the subfolders in the **PicturesLibrary** and list the name of each subfolder.

```cpp
//#include <ppltasks.h>
//#include <string>
//#include <memory>
using namespace Windows::Storage;
using namespace Platform::Collections;
using namespace concurrency;
using namespace std;

// Be sure to specify the Pictures Folder capability in the appxmanifext file.
StorageFolder^ picturesFolder = KnownFolders::PicturesLibrary;

// Use a shared_ptr so that the string stays in memory
// until the last task is complete.
auto outputString = make_shared<wstring>();
*outputString += L"Files:\n";

// Get a read-only vector of the file objects
// and pass it to the continuation. 
create_task(picturesFolder->GetFilesAsync())        
    // outputString is captured by value, which creates a copy 
    // of the shared_ptr and increments its reference count.
    .then ([outputString] (IVectorView<StorageFile^>^ files)
{        
    for ( unsigned int i = 0 ; i < files->Size; i++)
    {
        *outputString += files->GetAt(i)->Name->Data();
        *outputString += L"\n";
    }
})
    // We need to explicitly state the return type 
    // here: -> IAsyncOperation<...>
    .then([picturesFolder]() -> IAsyncOperation<IVectorView<StorageFolder^>^>^ 
{
    return picturesFolder->GetFoldersAsync();
})
    // Capture "this" to access m_OutputTextBlock from within the lambda.
    .then([this, outputString](IVectorView<StorageFolder^>^ folders)
{        
    *outputString += L"Folders:\n";

    for ( unsigned int i = 0; i < folders->Size; i++)
    {
        *outputString += folders->GetAt(i)->Name->Data();
        *outputString += L"\n";
    }

    // Assume m_OutputTextBlock is a TextBlock defined in the XAML.
    m_OutputTextBlock->Text = ref new String((*outputString).c_str());
});
```


<!--HONumber=May16_HO4-->


