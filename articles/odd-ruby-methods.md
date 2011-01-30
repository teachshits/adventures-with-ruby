I recently encountered some methods I didn't know about.

<h2>~</h2>

The tilde method (<tt>~</tt>) is used by <a href="http://sequel.rubyforge.org/">Sequel</a> and you can use it like this:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#96cbfe">class</font>&nbsp;<font color="#ffffb6">Post</font>
&nbsp;&nbsp;<font color="#96cbfe">def</font>&nbsp;<font color="#ffd2a7">~</font>
&nbsp;&nbsp;&nbsp;&nbsp;<font color="#ff73fd">11</font>
&nbsp;&nbsp;<font color="#96cbfe">end</font>
<font color="#96cbfe">end</font>

post = <font color="#ffffb6">Post</font>.new
~post <font color="#7c7c7c"># =&gt; 11</font></pre>

That's right: you call this method by placing the tilde <strong>before</strong> the object.

In Sequel it is used to perform NOT queries, by defining the tilde on Symbol:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#ffffb6">Post</font>.where(~<font color="#99cc99">:deleted_at</font>&nbsp;=&gt; <font color="#99cc99">nil</font>)
<font color="#7c7c7c"># =&gt; SELECT * FROM posts WHERE deleted_at IS NOT NULL</font></pre>

<h2>-@</h2>

The minus-at (<tt>-@</tt>) method works just about the same as the tilde method. It is the method called when a minus-sign is placed <strong>before</strong> the object. In effect, this means that Fixnum is implemented somewhere along the lines of this:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black"><font color="#96cbfe">class</font>&nbsp;<font color="#ffffb6">Fixnum</font>
&nbsp;&nbsp;<font color="#96cbfe">def</font>&nbsp;<font color="#ffd2a7">-@</font>
&nbsp;&nbsp;&nbsp;&nbsp;<font color="#99cc99">self</font>&nbsp;* -<font color="#ff73fd">1</font>
&nbsp;&nbsp;<font color="#96cbfe">end</font>
<font color="#96cbfe">end</font>

num = <font color="#ff73fd">10</font>
negative = -num <font color="#7c7c7c"># =&gt; -10</font></pre>

I found this one browsing through the source of the <tt><a href="http://github.com/rails/rails/blob/master/activesupport/lib/active_support/duration.rb#L34-36">ActiveSupport::Duration</a></tt> class (you know, the one you get when you do <tt>1.day</tt>). I guess it makes sense.

Be careful with chaining methods though:

<pre style="background: #000000; color: #f6f3e8; font-family: Monaco, monospace" class="ir_black">
ruby-1.9.1-p378 > num = 5
 => 5
ruby-1.9.1-p378 > -num.to_s
NoMethodError: undefined method `-@' for "5":String
  from (irb):5
  from /Users/iain/.rvm/rubies/ruby-1.9.1-p378/bin/irb:17:in `<main>'
</pre>

This also applies to the tilde method.

<h2>So?</h2>

I don't know. Enrich your DSLs and APIs, if it makes any sense to do it.