#Lab Report 3

Failure-inducing input:
```
    @Test
    public void testGetFilesFailure() throws IOException {
        File testDir = new File("testDirectory");
        testDir.mkdir();
        
        File file1 = new File(testDir, "file1.txt");
        file1.createNewFile();
        
        List<File> fileList = FileUtil.getFiles(testDir);
        
        assertTrue(fileList.contains(testDir));
        assertFalse(fileList.contains(file1)); // Expecting no duplication
        
        testDir.delete();
```
---
Non-failure-inducing input:
```
    @Test
    public void testGetFilesNonFailure() throws IOException {
        File testDir = new File("testDirectory");
        testDir.mkdir();
        
        File file1 = new File(testDir, "file1.txt");
        file1.createNewFile();
        
        List<File> fileList = FileUtil.getFiles(file1);
        
        assertTrue(fileList.contains(file1));
        assertFalse(fileList.contains(testDir)); // Expecting no duplication
        
        testDir.delete();
    }

```
---

