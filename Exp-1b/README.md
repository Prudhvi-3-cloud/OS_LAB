## Simulate UNIX commands like cp, ls, grep, etc
### Program Statemnt: To simulate UNIX command like cp,ls,grep
### Source Code:
### Cp simulate command Source code
```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
void simulate_cp(const char *source, const char *destination) {
FILE *src = fopen(source, &quot;r&quot;);
FILE *dest = fopen(destination, &quot;w&quot;);
if (!src || !dest) {
perror(!src ? &quot;Error opening source file&quot; : &quot;Error opening destination file&quot;);
if (src) fclose(src);
return;
}
char buffer[1024];
size_t bytes;
while ((bytes = fread(buffer, 1, sizeof(buffer), src)) &gt; 0) {
fwrite(buffer, 1, bytes, dest);
}
printf(&quot;File &#39;%s&#39; copied to &#39;%s&#39;\n&quot;, source, destination);
fclose(src);
fclose(dest);
}
int main(int argc, char *argv[]) {
if (argc != 3) {
fprintf(stderr, &quot;Usage: %s &lt;source_file&gt; &lt;destination_file&gt;\n&quot;, argv[0]);

return EXIT_FAILURE;
}
simulate_cp(argv[1], argv[2]);
return EXIT_SUCCESS;
}
```
### Interpretation of program:
1) The program takes the two command-line arguments: source-file and destination-file
2) It open the source file in read-only mode (&quot;r&quot;)
3) It open the destination file in write only mode(&quot;w&quot;).
4) If either file cannot be opened. It prints an error message and exits.
5) It reads the contents of the source file in chunks of 1024 bytes using fread.
6) It writes each chunk to the destination file using fwrite.
7) It writes once the entire source file has been copied, it prints a succes manager

### Output of the code for cp
![ Program output in console](copy.png)

&gt; ### Simulation code for ls command
```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;dirent.h&gt;
void simulate_ls(const char *path) {
struct dirent *entry;
DIR *dir = opendir(path);
if (!dir) {
perror(&quot;Error opening directory&quot;);
return;

}
while ((entry = readdir(dir)) != NULL) {
if (entry-&gt;d_name[0] != &#39;.&#39;) {
printf(&quot;%s &quot;, entry-&gt;d_name);
}
}
printf(&quot;\n&quot;);
closedir(dir);
}int main(int argc, char *argv[]) {
const char *path = argc &gt; 1 ? argv[1] : &quot;.&quot;;
simulate_ls(path);
return 0;
}
```
### Interpretion of Program:
1. The program takes an optimal command-line argument: the path to the directory to list.
2. If no argument is provided, it defaults to the current working directory (.).
3. It opens the specified directory using opendir.
4. If the directory cannot be opened, it prints an error using perror.
5. It reads the directory entries using readdir and prints the names of the files and
directories, executing hidden files.
6. Finally, it closes the directory using closedir

### Output of the code for ls
![ Program output in console](ls.png)

&gt; ### Simulate Grep command
```c
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;

#include &lt;string.h&gt;
void simulate_grep(const char *pattern, const char *filename) {
FILE *file = fopen(filename, &quot;r&quot;);
if (!file) {
perror(&quot;Error opening file&quot;);
return;
}
char line[1024];
while (fgets(line, sizeof(line), file)) {
if (strstr(line, pattern)) { // Check if pattern exists in the line
printf(&quot;%s&quot;, line);
}
}
fclose(file);
}int main(int argc, char *argv[]) {
if (argc != 3) {
fprintf(stderr, &quot;Usage: %s &lt;pattern&gt; &lt;filename&gt;\n&quot;, argv[0]);
return EXIT_FAILURE;
}
simulate_grep(argv[1], argv[2]);
return EXIT_SUCCESS;
}
```
### Interpretation Program:
1. The program takes two command-line arguments: the paltern to search for and the file
name to search in
2. It opens the specified file in read-only mode(&quot;r&quot;).
3. If the file cannot be opened, it prints an error message perror
4. It reads the file line by line using fgets.
5. For each line, it checks if the specified pattern exists using strstr.

6. If the pattern is found, it prints the entire line.
7. finally, it closes the file using fclose.

### Output of the code for grep
![ Program output in console](grep.png)

### Result: Thus the study and execution of UNIX commands like cp,ls,grep has been
completed successfully
