---
layout: home
---

Follow the [quick start guide](#quick-start) below to get started.

[![FAB Example](assets/example_FAB.png)](examples#View)

[JavaDocs](javadocs), [examples](examples) and a [sample app](https://github.com/sjwall/MaterialTapTargetPrompt/tree/master/sample/src/main/java/uk/co/samuelwall/materialtaptargetprompt/sample) with examples implemented are available.
The sample app is available to download on the Google Play Store:
<a href='https://play.google.com/store/apps/details?id=uk.co.samuelwall.materialtaptargetprompt.sample&utm_source=global_co&utm_medium=prtnr&utm_content=Mar2515&utm_campaign=PartBadge&pcampaignid=MKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1'><img alt='Get it on Google Play' style='max-width:90px' src='assets/play_store.png'/></a>

# Quick start

## Gradle

Add the following to build.gradle:

```groovy
repositories {
    jcenter()
}

dependencies {
    implementation 'uk.co.samuelwall:material-tap-target-prompt:{{ site.github.latest_release.tag_name | remove_first: "v" }}'
}
```
Supports Android minSdkVersion 14

## Usage

Tap target prompts are created with a [builder](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.Builder.html) class much like the Android AlertDialog builder:

```java
builder = new MaterialTapTargetPrompt.Builder(MainActivity.this)
```

Set the view to focus the prompt on:

```java
builder.setTarget(R.id.target_view_id)
```

Set the text to display on the first line:

```java
builder.setPrimaryText("This text is displayed on the first line")
```


Optionally set the text to display on the second line. If the primary text is not set the secondary text must be set 

```java
builder.setSecondaryText("Text to display on the second line")
```

To listen in to the prompt events set a PromptStateChangeListener.
Possible states are:
* [STATE_NOT_SHOWN](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_NOT_SHOWN) - Prompt has yet to be shown
* [STATE_REVEALING](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_REVEALING) - Prompt reveal animation is running
* [STATE_REVEALED](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_REVEALED) - Prompt reveal animation has finished and the prompt is displayed
* [STATE_FOCAL_PRESSED](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_FOCAL_PRESSED) - Prompt target has been pressed
* [STATE_NON_FOCAL_PRESSED](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_NON_FOCAL_PRESSED) - Prompt has been pressed outside the focal area
* [STATE_DISMISSING](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_DISMISSING) - Prompt dismiss method has been called and the prompt is being removed from view
* [STATE_DISMISSED](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_DISMISSED) - Prompt has been removed from view after the prompt has either been pressed somewhere other than the prompt target or the system back button has been pressed
* [STATE_FINISHING](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_FINISHING) - Prompt finish method has been called and the prompt is being removed from view
* [STATE_FINISHED](javadocs/uk/co/samuelwall/materialtaptargetprompt/MaterialTapTargetPrompt.html#STATE_FINISHED) - Prompt has been removed from view after the prompt has been pressed in the focal area

```java
builder.setPromptStateChangeListener(new MaterialTapTargetPrompt.PromptStateChangeListener()
        {
            @Override
            public void onPromptStateChanged(MaterialTapTargetPrompt prompt, int state)
            {
                if (state == MaterialTapTargetPrompt.STATE_FOCAL_PRESSED)
                {
                    // User has pressed the prompt target
                }
            }
        })
```

The Builder extends abstract class [PromptOptions](javadocs/uk/co/samuelwall/materialtaptargetprompt/extras/PromptOptions.html) which contains more customisation options.

Finally show the tap target:

```java
builder.show()
```

All combined together:

```java
import uk.co.samuelwall.materialtaptargetprompt.MaterialTapTargetPrompt;

new MaterialTapTargetPrompt.Builder(MainActivity.this)
        .setTarget(R.id.target_view_id)
        .setPrimaryText("This text is displayed on the first line")
        .setSecondaryText("Text to display on the second line")
        .setPromptStateChangeListener(new MaterialTapTargetPrompt.PromptStateChangeListener()
        {
            @Override
            public void onPromptStateChanged(MaterialTapTargetPrompt prompt, int state)
            {
                if (state == MaterialTapTargetPrompt.STATE_FOCAL_PRESSED)
                {
                    // User has pressed the prompt target
                }
            }
        })
        .show();
```

### Note

If a target is not set or the target view could not be found or both the primary and secondary text are `null` then `builder.show` and `builder.create` will return `null`.

# Customisation

The library is designed with extendable classes to allow for maximum customisation. More details and examples are available [here](customisation).

# License
    Copyright (C) 2016-2018 Samuel Wall

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
