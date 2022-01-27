# Caleb Gilmore

I am a 22 year old college student, and while my major is Computer Science, I am currently working with a company in Japan to help me teach English there. I also do a lot of content creation, and love trying new things. 

![A picture of me](me.jpg)

---
| Activity | Where can you do it? | How expensive is it? |
| ---| --- | ---: |
| HEMA | You can practice hema, or european sword play, just about anywhere. As for places to learn, you would just need to look up a dojo near you. | This can range from about $20 to well over $200, depending on how much you enjoy it |
| Gaming | Gaming can be done from anywhere, and houses all sorts of people | How much you spend, depends on how competitive you are, or how much you generally enjoy it. You should expect to spend at least 400 on a console. I personally spend well over 3000 on my PC |
| Dancing | Truly something you can do anywhere, as long as there's a beat and a will to dance | This one is completely free! Only thing you need to pay is your time, as learning can be very time consuming |

---

## My favorite quotes

> "If you live for yourself, you've only got yourself to blame. So, I can't really blame anyone else, and I don't have any regrets." -*Kyoko Sakura*

> "If you're not 100% sure why you're doing it, you'll most definitely regret it later" -*Mami Tomoe*

---

# Z-function Algorithm

> "This algorithm finds all occurrences of a pattern in a text in linear time. Let length of text be n and of pattern be m, then total time taken is O(m + n) with linear space complexity. Now we can see that both time and space complexity is same as KMP algorithm but this algorithm is simpler to understand." [Source](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)

```
// A C++ program that implements Z algorithm for pattern searching
#include<iostream>
using namespace std;

void getZarr(string str, int Z[]);

// prints all occurrences of pattern in text using Z algo
void search(string text, string pattern)
{
	// Create concatenated string "P$T"
	string concat = pattern + "$" + text;
	int l = concat.length();

	// Construct Z array
	int Z[l];
	getZarr(concat, Z);

	// now looping through Z array for matching condition
	for (int i = 0; i < l; ++i)
	{
		// if Z[i] (matched region) is equal to pattern
		// length we got the pattern
		if (Z[i] == pattern.length())
			cout << "Pattern found at index "
				<< i - pattern.length() -1 << endl;
	}
}

// Fills Z array for given string str[]
void getZarr(string str, int Z[])
{
	int n = str.length();
	int L, R, k;

	// [L,R] make a window which matches with prefix of s
	L = R = 0;
	for (int i = 1; i < n; ++i)
	{
		// if i>R nothing matches so we will calculate.
		// Z[i] using naive way.
		if (i > R)
		{
			L = R = i;

			// R-L = 0 in starting, so it will start
			// checking from 0'th index. For example,
			// for "ababab" and i = 1, the value of R
			// remains 0 and Z[i] becomes 0. For string
			// "aaaaaa" and i = 1, Z[i] and R become 5
			while (R<n && str[R-L] == str[R])
				R++;
			Z[i] = R-L;
			R--;
		}
		else
		{
			// k = i-L so k corresponds to number which
			// matches in [L,R] interval.
			k = i-L;

			// if Z[k] is less than remaining interval
			// then Z[i] will be equal to Z[k].
			// For example, str = "ababab", i = 3, R = 5
			// and L = 2
			if (Z[k] < R-i+1)
				Z[i] = Z[k];

			// For example str = "aaaaaa" and i = 2, R is 5,
			// L is 0
			else
			{
				// else start from R and check manually
				L = i;
				while (R<n && str[R-L] == str[R])
					R++;
				Z[i] = R-L;
				R--;
			}
		}
	}
}

// Driver program
int main()
{
	string text = "GEEKS FOR GEEKS";
	string pattern = "GEEK";
	search(text, pattern);
	return 0;
}
```
[Source](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)