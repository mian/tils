<b>Managing projects with makefile</b>
<p>
Makefiles are special format files that automatically build and manage your projects using make utility

Why we use Makefile?
1) Language independent — the only dependency you need is Make tool.
2) Simpler and cleaner base syntax for defining targets compared to a shell script.

Today there are many different flavors of Make tool on different systems. Linux by default uses the GNU Make, Windows needs to have it installed separately or if you’re using WSL — Windows Subsystem for Linux, you can get a GNU Make via most Linux distributions. 
On macOS you can install and update it with</p>

<pre><code>
brew install make
</code>
</pre>
<p>
<b>Lets learn how make utility works</b>

If you run the command</p>

<pre><code>
make
</code>
</pre>

<p>
it will look for the file names as “Makefile” in your current directory and will run it

If you have multiple make files in the directory then you can run the specific file by this command</p>

<pre><code>
make -f myfile
</code>
</pre>

<p>
There are multiple switches to the make file you can run the command
</p>

<pre><code>
man make
</code>
</pre>
<p>
to get more details

Lets Create a very simple make file in the root directory for any of your project

</p>
<pre><code>
install:
 composer install
test:
 phpunit
foo:
 echo “bar”
 </code>
 </pre>
 
<p>
By default, Makefile needs tabs in front of the target commands. The install is the target name which can be executed from the command line with make install, and the next line(s) prefixed with a tab character define target steps.

To run the install target:
</p>

<pre><code>
make install
</code>
</pre>
 
 <p>
 same as if you want to run the tests then run this command
 </p>
 
  
<pre><code>
make test
</code>
</pre>

<p>
Here are few components in make file

<b>Character @</b>

Every time you run the make file it also output the command to prevent it outputting the command you can add @ in front of the 
command

Example :

</p>

<pre><code>
install:
 @composer install
</code>
</pre>

<p>
Default goal
Whenever you run make without specifying the target name it will try to execute the first target. You can avoid this by setting a special variable .DEFAULT_GOAL:
</p>

<pre><code>
.DEFAULT_GOAL := help
help:
 @echo “help needed”
</code></pre>

<p>
<b>Phony targets</b>

Make is by default dedicated to generating executable files from their sources.All target names are by default the names of the files in the project folder. The built-in .PHONY target defines targets which should execute their recipes even if the file with the same name as target is present in the project.

When you’re adding a Makefile in your project you should define all custom targets as phony to avoid issues if file with same name is present in the project.
</p>

<pre><code>
.DEFAULT_GOAL := help
.PHONY: test install
help:
 @echo “help needed”
test:
 @echo “Testing command here”
install:
 @echo “Installing command here”
</code></pre>

<p>
<b>Passing variables:</b>

Some targets might require additional variables. With Make you can use arguments make foo arg=value.
</p>

<pre><code>
.DEFAULT_GOAL := help
.PHONY: test install foo
help:
 @echo “help needed”
test:
 @echo “Testing command here”
install:
 @echo “Installing command here”
foo:
 @echo $(arg)
 @echo $(arg)
</code></pre>

<p>
Then you can run it like this
</p>

<pre><code>
make foo arg=bar
</code></pre>




