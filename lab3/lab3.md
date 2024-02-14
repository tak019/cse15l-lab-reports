#Lab Report 3
##Part 1
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
Fail Output:
![Image](fail.PNG)
---
Success Ouput:
![Image](succeed.PNG)
---
Before:
```
	static List<File> getFiles(File start) throws IOException {
	  File f = start;
	  List<File> result = new ArrayList<>();
	  result.add(start);
	  if(f.isDirectory()) {
	    File[] paths = f.listFiles();
	    for(File subFile: paths) {
	      result.add(subFile);
	    }
	  }
	  return result;
	}
}
```
---
After:
```
static List<File> getFiles(File start) throws IOException {
    List<File> result = new ArrayList<>();
    if(start.isDirectory()) {
        File[] paths = start.listFiles();
        for(File subFile: paths) {
            result.add(subFile);
        }
    }
    return result;
}
```
---
Explanation:
The bug is that the method `getFiles` adds the `start` file to the result list before checking if it's a directory. This results in duplication of the start file in the result list when `start` is a directory. In the fixed code, the `start` file is only added to the result list if it's a directory. This prevents duplication of the start file in the result list when processing directories.
