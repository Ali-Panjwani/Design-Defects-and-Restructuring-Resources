Definiton:  
A client should not be forced to depend on methods it does not use. This means that interfaces should be small and focused on a single purpose.  

Example:  
Suppose we have an interface for a document management system that includes methods for uploading, downloading, and searching documents. By following the ISP, we would create separate interfaces for each of these functionalities, so that clients can depend only on the methods they actually use.  

Code:  
```
public interface DocumentUploader {
    void upload(Document document);
}

public interface DocumentDownloader {
    Document download(String documentId);
}

public interface DocumentSearcher {
    List<Document> search(String query);
}

public class DocumentManagementSystem implements DocumentUploader, DocumentDownloader, DocumentSearcher {
    // Implement all three methods
}
```
