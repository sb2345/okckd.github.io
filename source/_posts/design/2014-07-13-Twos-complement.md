---
layout: post
title: "[Design] Two's complement"
comments: true
category: Design
tags: [  ]
---

### Overview

Two's complement is a binary signed number representation.

Negative values are taken by subtracting the number from 2^n. This is the most common method of representing signed integers on computers.

### Example

<table class="wikitable sortable jquery-tablesorter" style="text-align: center;">
<thead><tr>
<th class="headerSort bg-color bg-img font-color" tabindex="0" role="columnheader button" title="Sort ascending">Bits</th>
<th class="headerSort bg-color bg-img font-color" tabindex="0" role="columnheader button" title="Sort ascending">Unsigned value</th>
<th class="headerSort bg-color bg-img font-color" tabindex="0" role="columnheader button" title="Sort ascending">2's complement value</th>
</tr></thead><tbody>
<tr>
<td class="bg-color bg-img font-color">0111 1111</td>
<td align="right" class="bg-color bg-img font-color">127 </td>
<td align="right" class="bg-color bg-img font-color">127 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">0111 1110</td>
<td align="right" class="bg-color bg-img font-color">126 </td>
<td align="right" class="bg-color bg-img font-color">126 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">0000 0010</td>
<td align="right" class="bg-color bg-img font-color">2 </td>
<td align="right" class="bg-color bg-img font-color">2 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">0000 0001</td>
<td align="right" class="bg-color bg-img font-color">1 </td>
<td align="right" class="bg-color bg-img font-color">1 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">0000&nbsp;0000</td>
<td align="right" class="bg-color bg-img font-color">0 </td>
<td align="right" class="bg-color bg-img font-color">0 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">1111 1111</td>
<td align="right" class="bg-color bg-img font-color">255 </td>
<td align="right" class="bg-color bg-img font-color">−1 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">1111 1110</td>
<td align="right" class="bg-color bg-img font-color">254 </td>
<td align="right" class="bg-color bg-img font-color">−2 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">1000 0010</td>
<td align="right" class="bg-color bg-img font-color">130 </td>
<td align="right" class="bg-color bg-img font-color">−126 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">1000 0001</td>
<td align="right" class="bg-color bg-img font-color">129 </td>
<td align="right" class="bg-color bg-img font-color">−127 </td>
</tr>
<tr>
<td class="bg-color bg-img font-color">1000 0000</td>
<td align="right" class="bg-color bg-img font-color">128 </td>
<td align="right" class="bg-color bg-img font-color">−128 </td>
</tr>
</tbody><tfoot></tfoot></table>
<br/>

So basically '1111 1111' means -1, and '1000 0000' means -128. 
