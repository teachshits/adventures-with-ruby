This is a translation of <a href="http://blog.finalist.com/2010/04/12/quest-ce-que-cest-rubyesque/">the post I originally wrote down in Dutch</a> for my company.

I recently gave a presentation at my company Finalist IT Group about the philosophy behind Ruby. Code written with this philosophy in mind is called 'Rubyesque'. It's not hard science, so we had plenty ingredients for a discussion.

The reason behind the presentation was because we're in need of more Ruby developers and looked inside our own company for Java developers that want to learn Ruby. Because Java and the philosophy behind it are so radically different from Ruby, we organized a discussion to explore those differences.

<h3>About programming and the 'flow'</h3>

The Rubyesque mindset is all about opinions. Opinions tend to vary from person to person. By reading a lot of blogs and code I do see some sort of consensus. This opinion is not always explicitly mentioned, so I don't pretend to speak in absolute truths or be complete.

Programming is usually compared with other professions to give an idea what it's like to do it. Ruby programmers tend to compare programming with craftsmanship. I even go one step further. I think programming Ruby is a form of art of playing an instrument. Programming is a creative process. You're programming to express meaning and intent. The only way to achieve this, is if you know your instrument so intensely that it's not compromising you're ability to express yourself.

Every programming language has its own style. You can call it its 'flow'. It's wise to go with the flow. It's easier to use the language as it's intended to be used than to go against it. For example, don't try to force <a href="http://en.wikipedia.org/wiki/Class-based_programming">inheritance</a> in a language that is intended to be <a href="http://en.wikipedia.org/wiki/Prototype-based_programming">prototype based</a>. Program according to the flow and other programmers can understand and maintain your code better.

<h3>About Ruby</h3>

Everything in Ruby is aimed towards making the programmer happy. A happy programmer is better motivated to deliver great code and will feel responsible to do so. And better code makes everyone happy.

It's the machine that is supposed to do the heavy lifting, not the programmer. This means that Ruby isn't particularly fast, but since machine power is cheaper than man power, it's not that big of a deal.

Ruby has a couple of traits that make it a joy to work with:

<ul>
  <li>Dynamic and open to bend it to your liking</li>
  <li>Few rules, so easy to learn</li>
  <li>There are 'shortcuts' for common tasks</li>
  <li>Many ways to reuse code, such as mixins</li>
  <li>Optional punctuation to improve readability</li>
  <li>Methods like <tt><a href="http://www.rubyist.net/~slagell/ruby/accessors.html">attr_accessor</a></tt> to become more <a href="http://en.wikipedia.org/wiki/DRY">DRY</a></li>
</ul>

<h3>Dynamic</h3>

In a dynamic language it's not important to know which type of object you're dealing with, but it's more important to know what it can do for you. This is called <a href="http://en.wikipedia.org/wiki/Duck_typing">duck typing</a>. This isn't only handy in making mock object, but also means that you don't have to abuse inheritance to comply to some method you'd like to call.

A nice example is the Rack specification. The header object you're supposed to return needs to have the method <tt>each</tt>. It doesn't say that it needs to be a hash. You could use a hash, but if it makes more in your sense to have some other object, it's fine. You don't have to inherit from hash, just to implement the <tt>each</tt> method.

The <em>flow</em> in Ruby is not to perform any check of the objects. If you're explicitly want an integer, just call <tt>to_i</tt> inside the method. Any code that checks the type is usually considered to be distracting from the real meaning of the code. It's the programmer that uses the gem/library responsibility to use the right objects, and not the responsibility of the gem-maker. The naming of methods and variables need to be obvious enough, so that it shouldn't be a guessing game.

<h3>Open</h3>

In Ruby, nothing is final. This allows for the ability to add and change anything in any object, including core classes. This is called Monkey Patching or <a href="http://en.wikipedia.org/wiki/Duck_punching">duck punching</a>. This results in even nicer and more readable code, like:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#ff73fd">15</font>.minutes.ago</pre>


Nobody needs to explain this. Nobody needs to look up any documents to understand what is going on here. Monkey patching can improve the readability of the code immensely.

I understand that this technique may be considered extreme by some people. It doesn't comply to the strict rules that govern most other languages. Still, these kinds of techniques are very handy and addicting.

Monkey patching is dangerous. It's your own responsibility to use it responsible. Use tests to ensure that you don't break anything unintentionally.

<h3>Punctuation</h3>

Some of Ruby's punctuation is optional. Ruby programmers love to leave them out. It's mostly a matter of taste. Readability is key here.

Rubyists rather write this:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#96cbfe">class</font>&nbsp;<font color="#ffffb6">Post</font>
&nbsp;&nbsp;belongs_to <font color="#99cc99">:author</font>, <font color="#99cc99">:dependent</font>&nbsp;=&gt; <font color="#99cc99">:destroy</font>
<font color="#96cbfe">end</font></pre>

Than the same code with all punctuation visible:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#96cbfe">class</font>&nbsp;<font color="#ffffb6">Post</font>
&nbsp;&nbsp;belongs_to(<font color="#99cc99">:author</font>, {<font color="#99cc99">:dependent</font>&nbsp;=&gt; <font color="#99cc99">:destroy</font>})
<font color="#96cbfe">end</font></pre>

It's not important that <tt>{:dependent => :destroy}</tt> is a hash. Nor is it important that <tt>belong_to</tt> is a method, and that it takes two arguments. It's much more important that the post belongs to an author and that the post will be destroyed when the author is being destroyed.

By not using all the possible punctuation, it becomes easier for our brains to focus on <em>what</em> is actually written, rather that <em>which objects</em> might be used to express it.


<h3>Few rules, many shortcuts</h3>

There are only a few genuine language constructs. There are just three elements in the language that have any real meaning. Those are objects, methods and blocks/closures. The only way in which classes and modules are special is by their implementation, but they are still regular objects. There are just a few other constructs, most notably <tt>if</tt>, <tt>while</tt> and the logic operators like <tt>&&</tt> and <tt>||</tt>.

The rest of the keywords you see are just shortcuts, you can type to perform common tasks. Like defining a class:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#96cbfe">class</font>&nbsp;<font color="#ffffb6">Car</font>&nbsp;&lt; <font color="#ffffb6">Vehicle</font>
&nbsp;&nbsp;<font color="#7c7c7c"># ...</font>
<font color="#96cbfe">end</font></pre>

The Ruby interpreter reads this as:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#ffffb6">Car</font>&nbsp;= <font color="#ffffb6">Class</font>.new(<font color="#ffffb6">Vehicle</font>) <font color="#6699cc">do</font>
&nbsp;&nbsp;<font color="#7c7c7c"># ...</font>
<font color="#6699cc">end</font></pre>

Defining a class is actually just a method called on an object. The first argument is another object (the class to inherit from) and the second argument is a block. You can write it like this if you want to and play with it too, like dynamically making many different classes.

Some other examples:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black">counter += <font color="#ff73fd">1</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#7c7c7c"># this is a shortcut</font>
counter = counter + <font color="#ff73fd">1</font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#7c7c7c"># without the shortcut, but also without punctuation</font>
counter = counter.+(<font color="#ff73fd">1</font>)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#7c7c7c"># without the shortcut and with all punctuation (yes, + is just a method)</font></pre>

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#c6c5fe">@user</font>&nbsp;||= <font color="#ffffb6">User</font>.new&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#7c7c7c"># this is called a 'teapot'-operator or 'or-or-equals'</font>
<font color="#c6c5fe">@user</font>&nbsp;= <font color="#c6c5fe">@user</font>&nbsp;|| <font color="#ffffb6">User</font>.new&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#7c7c7c"># assign @user to @user if it exists, otherwise create a new user</font></pre>

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#6699cc">exit</font>&nbsp;<font color="#6699cc">unless</font>&nbsp;busy <font color="#6699cc">or</font>&nbsp;cancelled&nbsp;&nbsp;<font color="#7c7c7c"># 'unless' is a shortcut for 'if !()'</font>
<font color="#6699cc">exit</font>&nbsp;<font color="#6699cc">if</font>&nbsp;!(busy <font color="#6699cc">or</font>&nbsp;cancelled)&nbsp;&nbsp; <font color="#7c7c7c"># 'if' at the end of a sentence is also a shortcut</font>
<font color="#6699cc">if</font>&nbsp;!(busy <font color="#6699cc">or</font>&nbsp;cancelled)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#7c7c7c"># for a regular if</font>
&nbsp;&nbsp;<font color="#6699cc">exit</font>
<font color="#6699cc">end</font></pre>

There are many more shortcuts. But why? Why are there so many ways to do the same thing? It's not just readability, but also the ease in which you can translate the ideas in your head to code.

The smaller the difference between your thoughts and your code, the easier it is to program. Ruby gives you full freedom to express yourself how you feel fit. That doesn't mean it always works out. If you have an unclear image of the problem you're trying to solve, the code you write will be unclear too. Nothing stops you to write bad code. Ruby doesn't force you in any way. These things cut both ways.

<h3>Exposing intention</h3>

Code needs to expose its intent. Ruby code is Rubyesque if it uses the above mentioned techniques to expose its intent. Because Ruby has such clean syntax, most DSLs (Domain Specific Languages) will be written in Ruby. These kinds of DSLs are called internal.

The naming of variables and methods is extremely important. The meaning of the code must be clear the first time you read it.

A fantastic example is <a href="http://rspec.info">Rspec</a>, my favorite test framework.

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black">describe <font color="#ffffb6">Post</font>&nbsp;<font color="#6699cc">do</font>

&nbsp;&nbsp;context <font color="#336633">&quot;</font><font color="#a8ff60">when it's not approved</font><font color="#336633">&quot;</font>&nbsp;<font color="#6699cc">do</font>
&nbsp;&nbsp;&nbsp;&nbsp;subject { <font color="#ffffb6">Post</font>.new(<font color="#99cc99">:approved</font>&nbsp;=&gt; <font color="#99cc99">false</font>) }
&nbsp;&nbsp;&nbsp;&nbsp;it { should_not be_publishable }
&nbsp;&nbsp;<font color="#6699cc">end</font>

&nbsp;&nbsp;context <font color="#336633">&quot;</font><font color="#a8ff60">when it's approved</font><font color="#336633">&quot;</font>&nbsp;<font color="#6699cc">do</font>
&nbsp;&nbsp;&nbsp;&nbsp;subject { <font color="#ffffb6">Post</font>.new(<font color="#99cc99">:approved</font>&nbsp;=&gt; <font color="#99cc99">true</font>) }
&nbsp;&nbsp;&nbsp;&nbsp;it { should be_publishable }
&nbsp;&nbsp;<font color="#6699cc">end</font>

<font color="#6699cc">end</font></pre>

The entire Ruby bag of tricks is being used to make it as natural as possible to write down your specifications. This example doesn't like like regular Ruby code, but it still is. It's nothing more than objects, methods and blocks.

This is very Rubyesque. There is almost no distraction from the meaning of the code. I can plainly read if my code still does what my customer wants and I can run the specs to see if my code does what I specified it to do. And even nicer: it's incredibly easy! Rspec makes Test Driven Development very easy.

If you're interested in the code to implement this example, take a look at <a href="http://gist.github.com/362030">this gist</a>.
</p>

<h3>Succinct and Concise</h3>

Rubyesque code is succinct. That doesn't just mean short lines (I try to limit myself to about 80 or 100 characters per line), but also about short methods. The code smell detector <a href="http://wiki.github.com/kevinrutherford/reek/">Reek</a> will raise a warning if your method is longer than 6 lines. Does this means you are not allowed to write longer methods? Of course not. Is it a good idea? No.

People are better at understanding short sentences. And it's the people that need to understand the code and maintain. And we're back to the philosophy behind Ruby. It's meant to be understandable for people. It's less important if the computer needs to do some extra work.

<h3>Conclusion</h3>

Ruby is a free language. You can bend the rules. The goal is to make you happy. Ruby was made to make you happy, to close the gap between human and computer language. Try to do that in the code you write too, it works!

I found that most people coming from languages like Java or PHP find Ruby a weird or magical language. That is only the appearance. Ruby is very easy to learn. It has few rules. Ruby programmers don't code using rigid rules and dogmas, but experiment solving the same problem in different ways.

I hope you got some idea of what it means to program Rubyesque. I advise everybody to look at the different languages and their philosophies. See what philosophy suits you. If the Ruby philosophy suits you and you have the discipline needed to write Ruby, give it a try! Ruby transformed the way I feel about my job and never regretted learning it one bit.