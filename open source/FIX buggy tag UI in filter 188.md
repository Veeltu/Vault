https://github.com/ClimateTown/knowledge-hub/pull/188

CimateTown.

## Describe your changes

I changed the structure of the code and the css to work as described. Now it is working

## Related issue number/link

Closes [#182](https://github.com/ClimateTown/knowledge-hub/issues/182)

The tags in the filter are buggy such that only clicking in the blue area (checkbox or on the text itself) activates the tag.

Expected behavior  
A click anywhere in the tag area activates the tag.

===

I change size of input/checkbox to match full div/ same size.

```js
  {#each tags as tag}
                <!-- checkboxes -->
                <div class="flex justify-between gap-2 rounded-full bg-gray-300" >
                    <label class="cursor-pointer +py-2 px-3 rounded-full+ flex items-center gap-2" for={removeWhitespace(tag)}>
                      <input
                        type="checkbox"
                        class="appearance-none cursor-pointer w-6 h-6 bg-white rounded-full checked:bg-black transition duration-200"
                        bind:checked={filterObject.tags[tag]}
                        id={removeWhitespace(tag)}
                        name={removeWhitespace(tag)}
                      />
                      <span>{tag}</span>
                    </label>
                  </div>
            {/each}
`````




