# VUE

## Template

#### Use component self-closing tag if there is no slots

###### Bad:
```
  <Component></Component>
```
###### Good:
```
  <Component />
```
<br><br>


#### If there is more than 2 props split them in multiple lines and follow [props order](https://vuejs.org/v2/style-guide/#Element-attribute-order-recommended)

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


#### Use double quotes in `template` and single in `script`

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


#### Use computed property instead of conditions

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


#### Always use `key` with `v-for`

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


#### Passing slots

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


#### Split a lot of markup with comments

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

## Script

#### Use single quotes and backticks instead of double quotes

###### Bad:
```
  foo: "",
  bar: slug + "/files"
```
###### Good:
```
  foo: '',
  bar: `${slug}/files`
```
<br><br>


#### Follow imports order

###### Bad:
```
import { mapActions, mapGetters } from 'vuex'
import { required } from 'vuelidate/lib/validators'
import lodash from 'lodash'
import NewFormInterpritation from './NewFormInterpritation'
import preparePayload from '@/utils/preparePayload'
import { merge, path, pathOr, isEmpty } from 'ramda'
```
###### Good:
```
// Vuex
import { mapActions, mapGetters } from 'vuex'

// Components
import NewFormInterpritation from './NewFormInterpritation'
import CustormFormField from './NewCustormFormField'

// Libs, utils, modules
import { required } from 'vuelidate/lib/validators'
import { merge, path, pathOr, isEmpty } from 'ramda'
import preparePayload from '@/utils/preparePayload'
import lodash from 'lodash'
```
<br><br>


#### Follow component [options order](https://vuejs.org/v2/style-guide/#Component-instance-options-order-recommended)

###### Bad:
```
components
name
data
methods
mounted
created
props
computed
// ...
```
###### Good:
```
name
components
mixins
props
data
computed
watch
methods
lifecycle methods in order they are called
```
<br><br>


#### Split actions and getters into multiple lines while mapping

###### Bad:
```
...mapGetters(['agendaSettings', 'locationsList', 'sessionsList', 'totalSessionsPages', 'totalSessionsItems'])
```
###### Good:
```
...mapGetters([
  'agendaSettings',
  'locationsList',
  'sessionsList',
  'totalSessionsPages',
  'totalSessionsItems'
])
```
<br><br>


#### Avoid "Can not read prop of undefined". Use [ramda pathOr method](http://ramdajs.com/docs/#pathOr) or atleast do check

###### Bad:
```
object.nested.prop
```
###### Good:
```
pathOr('', ['nested', 'prop'], object)
```
```
if (object && object.nested) {
  object.nested.prop
}
```
<br><br>


#### Do NOT mutate. Use [ramda clone](http://ramdajs.com/docs/#clone) or ES6 destructure

###### Bad:
```
1. Object copy
obj1 = obj2

2. Array copy
arr1 = arr1

3. Add item
arr.push()

4. Remove item
arr.splice(2, 1)
```
###### Good:
```
1. Object copy
obj1 = clone(obj2)
obj1 = { ...obj2 }

2. Array copy
arr1 = [...arr2]

3. Add item
arr = [...arr, newItem]

4. Remove item
arr = arr.filter((item, i) => i !== indexToDelete)
```
<br><br>


#### Use ternary operator

###### Bad:
```
if (condition) {
  return a
} else {
  return b
}
```
###### Good:
```
return condition
  ? a
  : b
```
<br><br>


#### Don't forget to stop listening for eventBus event in beforeDestroy

###### Bad:
```
created () {
  // start listening
  this.$bus.$on('modalChangeVisibility', ...)
}
```
###### Good:
```
created () {
  // start listening
  this.$bus.$on('modalChangeVisibility', ...)
},
beforeDestroy () {
  // stop listening (don't pass callback in $off)
  this.$bus.$off('modalChangeVisibility')
}
```
<br><br>


## Vuex

#### Mostly start mutation name from `SET`

###### Bad:
```
[types.GET_FOO]
[types.NAME_FOO]
[types.FOO]
```
###### Good:
```
[types.SET_FOO]
[types.UPDATE_FOO]
[types.ADD_TO_FOO]
```
<br><br>


#### Mostly start action name from `fetch`, `post`, `update`, `delete`

###### Bad:
```
getItems
itemDelete
```
###### Good:
```
fetchItems
updateItem
deleteItem
```
<br><br>
