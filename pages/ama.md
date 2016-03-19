---
layout: page
title: AMA
permalink: /ama/
---		
<style>
.container {
    max-width: 60rem !important;
    font-size: 0.9em;
}
tr.question {
	background-color: #FFFDE3 !important;
}
tr.user-nemo {
	background-color: #EDF8FF !important;
}
tr:nth-child(odd) td{
    background-color: inherit !important;
}
.ts {
	min-width: 90px;
    font-size: 12px;
}
.emoji {
	display: inline;
}
</style>

This is a transcript of an AMA (Ask Me Anything) session I recently did on the Developers & Hackers Slack Channel.

- You can join the slack team [via this link](https://slackipy-codetogether.rhcloud.com).
- The AMA lasted for a week from 4-11 March 2016
- This is a slightly edited, condensed version of the AMA with a lot of extra messages removed and cleaned.
You can access the original at [slackarchive](https://dev-s.slackarchive.io/ama/)
- All timestamps are in IST and were extracted using the Slack
- You can find the YML file used to generate this page at [GitHub](https://github.com/captn3m0/captn3m0.github.com/blob/master/_data/projects.yml)

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Thought I&#39;d draw something for my tiny <a href="https://twitter.com/hashtag/AMA?src=hash">#AMA</a>. See pinned tweet for the details. <a href="https://t.co/U9r3vqJ8Yj">pic.twitter.com/U9r3vqJ8Yj</a></p>&mdash; Nemo (@captn3m0) <a href="https://twitter.com/captn3m0/status/705822087735177216">March 4, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<table>
<thead>
	<tr>
		<th>user</th>
		<th>message</th>
		<th class="ts">time</th>
		
	</tr>
</thead>
<tbody>
	{% for section in site.data.ama %}{% for message in section %}{% if forloop.index0 == 0 %}
	<tr class="question">
		<td>{{message.user}}</td>
		<td>{{message.text | markdownify}}</td>
		<td class="ts">{{message.timestamp | date:"%F %R"}}</td>
		
	</tr>
	{% else %}
	<tr class="user-{{message.user}}">
		<td>{{message.user}}</td>
		<td>{{message.text |markdownify}}</td>
		<td class="ts">{{message.timestamp | date:"%F %R"}}</td>
		
	</tr>
	{% endif %}
{% endfor %}
{% endfor %}
</tbody>

</table>

If you've reached this and are still reading, here's an easter egg for you<a href="https://www.youtube.com/watch?v=BVT-ChnS_Mg" rel="nofollow">:</a> I named myself Nemo after Capt. Nemo in 20,000 leagues under the sea.