---
layout: post
title: "TS刷题常用API: String"
subtitle: "Commonly used TypeScript/JavaScript API for LeetCode - String related"
date: 2022-08-07
author: "代码笔记哥"
header-img:
tags:
  - 算法
  - JS
  - API
  - Extensible Note
---

WIP:

<!-- Language Selector -->
<select onchange= "onLanChange(this.options[this.options.selectedIndex].value)">
    <option value="0" selected> English 英语 </option>
    <option value="1"> 中文 Chinese </option>
</select>

<!-- Chinese Version -->
<div class="zh post-container">
    <h3>前言</h3>
    <p>本文提供笔记哥用 JavaScript/TypeScript 刷题时的常用的 String 相关的的 API。<br>
    方便阅读和快速理解，本文尽量提供这些 API 的中文注解。</p>

    <h3> 1. 基于一个 string 类型的操作</h3>
    <ol>
        <li>获取 substring</li>
    </ol>
    <pre>
        <code>str.substring(i, j); //获取首字符位于index i，末字符位于index j-1的substring</code>
    </pre>

    <h3>总结</h3>
    <p>您还有什么要补充的 JavaScript/TypeScript 刷题常用的 String 类 API 吗？如果 YES，请留言，不吝赐教。</p>

</div>

<!-- English Version -->
<div class="en post-container">
    <h3>Preface</h3>
    <p>This article provides the common JavaScript/TypeScript API for String when you are LeetCoding.</p>

    <h3> 1. Operations on a string</h3>
    <ol>
        <li>Obtain a substring from the given string</li>
    </ol>
    <pre>
        <code>str.substring(i, j); // Obtain a substring whose starting index is i and ending index is j-1</code>
    </pre>

    <h3>Summary</h3>
    <p>Please share more JavaScript/TypeScript common API for String during LeetCoding in the comment section below. Thak you.</p>

</div>

<!-- Handle Language Change -->
<script type="text/javascript">
    var $zh = document.querySelector(".zh");
    var $en = document.querySelector(".en");
    function onLanChange(index) {
        if (index == 0) {
            /* 0 - English */
            $en.style.display = "block";
            $zh.style.display = "none";
        } else {
            $zh.style.display = "block";
            $en.style.display = "none";
        }
    }
    onLanChange(0);
</script>
