## test_assignment

### Build
<pre><code class="shell">   make</code></pre>

### Install
<pre><code class="shell">#  insmod dmp.ko</code></pre>


### Test

First create the example device and proxy device by doing

<pre><code class="shell">#  dmsetup create zero1 --table "0 _SIZE_ zero" # You should define the _SIZE_</code></pre>
<pre><code class="shell">#  dmsetup create dmp1  --table "0 _SIZE_ dmp /dev/mapper/zero1"</code></pre>

Then make sure everything was successfully created with
<pre><code class="shell">#  dmsetup ls</code></pre>
Or
<pre><code class="shell">$  ls -al /dev/mapper/*</code></pre>

After try to read and write to a proxy device
<pre><code class="shell">#  dd if=/dev/random of=/dev/mapper/dmp1 bs=4k count=1</code></pre>
<pre><code class="shell">#  dd of=/dev/null if=/dev/mapper/dmp1 bs=4k count=1</code></pre>

For statistics
<pre><code class="shell">#  cat /sys/module/dmp/stat/volumes</code></pre>


### Remove
<pre><code class="shell">First you need to remove created devices, so run
#  dmsetup remove dmp1 zero1

Then unload the module
#  rmmod dmp

And clean src directory
make clean
</code></pre>
