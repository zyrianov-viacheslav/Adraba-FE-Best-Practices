## Templates

##### 1. Use component self-closing tag if there is no slots

###### Bad:
```
  <Component></Component>
```
###### Good:
```
  <Component />
```
<br><br>


##### 2. If there is more than 2 props split them in multiple lines and follow [props order](https://vuejs.org/v2/style-guide/#Element-attribute-order-recommended)

###### Bad:
```
  <Component @click="handleClick" :type="foo" :theme="bar" v-else @change="handleChange" :active="false" />
```
```
  <Component @click="handleClick"
             :type="foo"
             :theme="bar"
             v-else
             @change="handleChange"
             :active="false"></Component>
```
###### Good:
```
  <Component
    v-else
    :active="false"
    :type="foo"
    :theme="bar"
    @change="handleChange"
    @click="handleClick"
  />
```
<br><br>


##### 3. Use double quotes in `template` and single in `script`

###### Bad:
```
  <Component type='foo' class="bar" />
```
###### Good:
```
  <Component
    type="foo"
    class="bar"
  />
```
<br><br>


##### 4. Use computed property instead of conditions

###### Bad:
```
  <Component v-if="accessToken && user.data" />
```
###### Good:
```
  <Component v-if="isLogedIn" />

  // ...
  isLogedIn () {
    return accessToken && user.data
  }
```
<br><br>


##### 5. Always use `key` with `v-for`

###### Bad:
```
  <Component v-for="item in items" />
```
###### Good:
```
  <Component
    v-for="(item, i) in items"
    :key="`item-${i}`"
  />
```
<br><br>


##### 6. Passing slots

###### Bad:
```
  <Component
    @click="handleClick"
    :active="false"
    :type="foo">Submit</Component>
```
```
  <Component
    @click="handleClick"
    :active="false"
    :type="foo"
  >Submit</Component>
```
###### Good:
```
  <Component
    :active="false"
    :type="foo"
    @click="handleClick"
  >
    Submit
  </Component>
```
<br><br>


##### 7. Split a lot of markup with comments

###### Bad:
```
<div v-if="isRegular" class="related-session-inner_regular">
  <h4 class="related-session-inner__header">
    {{ time }}
  </h4>
  <p class="related-session-inner__body" v-html="shortDescriptionCuted"></p>
  <div
    class="related-session__translation-icon"
    v-html="translationIcon"
    v-if="sessionData.metadata.translator"
  ></div>
</div>
<div v-if="isFeatured" class="related-session-inner_featured">
  <div class="related-session-inner_featured-content">
    <h4 class="related-session-inner__header">
      {{ time }}
    </h4>
    <p class="related-session-inner__body">
      {{ title }}
    </p>
  </div>
  <div
    class="related-session-inner_featured-logo"
    :style="logoStyles"
  >
  </div>
</div>
```

###### Good:
```
<!-- REGULAR ITEM -->
<div v-if="isRegular" class="related-session-inner_regular">
  <h4 class="related-session-inner__header">
    {{ time }}
  </h4>
  <p class="related-session-inner__body" v-html="shortDescriptionCuted"></p>
  <div
    class="related-session__translation-icon"
    v-html="translationIcon"
    v-if="sessionData.metadata.translator"
  ></div>
</div>
<!-- REGULAR ITEM -->

<!-- FEATURED ITEM -->
<div v-if="isFeatured" class="related-session-inner_featured">
  <div class="related-session-inner_featured-content">
    <h4 class="related-session-inner__header">
      {{ time }}
    </h4>
    <p class="related-session-inner__body">
      {{ title }}
    </p>
  </div>
  <div
    class="related-session-inner_featured-logo"
    :style="logoStyles"
  >
  </div>
</div>
<!-- FEATURED ITEM -->
```
<br><br>