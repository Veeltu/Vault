ClimateTown

https://github.com/ClimateTown/knowledge-hub/issues/187

**Describe your suggested improvement**  
Add simple resource metrics to the resource page, including:

1.  Number of resources (e.g. `42 resources and counting!!`)
2.  Number of resources belonging to a tag (this can be placed straight after the tag text in a lighter color. E.g. `Climate Journalism (4)`)

[![image](https://user-images.githubusercontent.com/36369090/238191439-be5f83e4-577d-451c-bb0a-3dce51f40607.png)](https://user-images.githubusercontent.com/36369090/238191439-be5f83e4-577d-451c-bb0a-3dce51f40607.png)

**Describe the benefit**  
Provides a better insight to users of how many resources there are in the hub, and what their distribution is between tags. Also provides an easy metric for moderators to see which tags aren't used as much (perhaps leading to consolidating tags, or focusing on finding more good resources for an under-represented tag).

**Would you be capable/willing to implement the improvement?**  
No, I currently have other focusses. Happy for someone to take a shot at this.

**Additional comments**  
Additional metrics may be useful. If you have any ideas, feel free to discuss.

==

HOW IT WORKS ?
```js
// create list of unique tags with count
let tag_count: { [key: string]: number } = {};

for (const tag of tags) {
tag_count[tag] = 0;
}
```
1. tag_count to obiekt key:string : a druga wartość to liczba.
2. pętla która iteruje tablicę "tags", gdzie elementami są "tag"
4. przypisuje do każdego elementu "tag" : tags__count o wartości 0
	1.  Dla każdego elementu `tag` z tablicy `tags`:
	    -   Tworzona jest właściwość `tag` w obiekcie `tag_count`.
	    -   Przypisywana jest wartość `0` do właściwości `tag_count[tag]`.
```js

for (const resource of yml_data) {
	for (const tag of resource.tags) {
		tag_count[tag] += 1;
	}
}
```
1. iteiruje przed "ytml_data" gdzie el= resource
2. w tym resource iteruje przez resource.tags (czyli tagi tam zapisane)
3. i dla każddego elementu tag_count[tag] dodaje 1
Przebieg pętli wygląda następująco:

1.  Dla każdego elementu `resource` z tablicy `yml_data`:
    -   Dla każdego elementu `tag` z tablicy `resource.tags`:
        -   Zwiększana jest wartość właściwości `tag_count[tag]` o `1`.



```js
// import tags from backend
let tags_count = data.payload.tags_count;
// html

{#each Object.entries(tags_count) as [tag_name, tag_count]}

	{#if tag == tag_name}{tag_name}: ({tag_count}) {/if}

{/each}


```

BETTER WAY - HOW IT WORKS ?

```js
//I think this would be better? It is a `key: value` structure after all
{tag} ({tags_count[tag]})
```
to znaczy : rendet tag i tag_count które ma taki sam tag