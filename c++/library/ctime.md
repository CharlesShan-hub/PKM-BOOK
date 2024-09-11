---
icon: clock
---

# ctime

## APIs

<table><thead><tr><th width="298">Time manipulation - Functions</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://cplusplus.com/reference/ctime/clock/"><strong>clock</strong></a></td><td>Clock program (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/difftime/"><strong>difftime</strong></a></td><td>Return difference between two times (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/mktime/"><strong>mktime</strong></a></td><td>Convert tm structure to time_t (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/time/"><strong>time</strong></a></td><td>Get current time (function)</td></tr></tbody></table>

<table><thead><tr><th width="298">Conversion - Functions</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://cplusplus.com/reference/ctime/asctime/"><strong>asctime</strong></a></td><td>Convert tm structure to string (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/ctime/"><strong>ctime</strong></a></td><td>Convert time_t value to string (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/gmtime/"><strong>gmtime</strong></a></td><td>Convert time_t to tm as UTC time (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/localtime/"><strong>localtime</strong></a></td><td>Convert time_t to tm as local time (function)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/strftime/"><strong>strftime</strong></a></td><td>Format time as string (function)</td></tr></tbody></table>

<table><thead><tr><th width="298">Macro constants</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://cplusplus.com/reference/ctime/CLOCKS_PER_SEC/"><strong>CLOCKS_PER_SEC</strong></a></td><td>Clock ticks per second (macro)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/NULL/"><strong>NULL</strong></a></td><td>Null pointer (macro)</td></tr></tbody></table>

<table><thead><tr><th width="298">types</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://cplusplus.com/reference/ctime/clock_t/"><strong>clock_t</strong></a></td><td>Clock type (type)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/size_t/"><strong>size_t</strong></a></td><td>Unsigned integral type (type)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/time_t/"><strong>time_t</strong></a></td><td>Time type (type)</td></tr><tr><td><a href="https://cplusplus.com/reference/ctime/tm/"><strong>struct tm</strong></a></td><td>Time structure (type)</td></tr></tbody></table>

## Demos

<details>

<summary>Delay</summary>

<pre class="language-cpp"><code class="lang-cpp">// waiting.cpp -- using clock() in a time-delay loop
#include &#x3C;iostream>
#include &#x3C;ctime> // describes clock() function, clock_t type
int main()
{
    using namespace std;
    cout &#x3C;&#x3C; "Enter the delay time, in seconds: ";
    float secs;
    cin >> secs;
    clock_t delay = secs * <a data-footnote-ref href="#user-content-fn-1">CLOCKS_PER_SEC</a>;  // convert to clock ticks
    cout &#x3C;&#x3C; "starting\a\n";
    clock_t start = clock();
    while (clock() - start &#x3C; delay )        // wait until time elapses
        ;                                   // note the semicolon
    cout &#x3C;&#x3C; "done \a\n";
    // cin.get();
    // cin.get();
    return 0; 
}

</code></pre>

</details>

## Reference

\[1] [https://cplusplus.com/reference/ctime/](https://cplusplus.com/reference/ctime/)

[^1]: in ctime
