---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
zoom: 100%

style: |
  .small-text {
    font-size: 0.45rem;
  }
  .smaller-text {
    font-size: 0.8rem;
  }
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---


# (Very) Quick and (Very) Dirty Intro to Cucumber 
# ![bg right:40% 80%](https://i.pinimg.com/originals/dd/be/20/ddbe20664a0e1e16a5706655616ee870.png)

---
# Agenda
- Very speedy intro
- Demo project
- Questions 
    -  <p class="small-text">That I may or may not know the answers to 😅</p>

---
# What?
- BDD testing framework <!--* BDD - Behaviour Driven Development-->
    - Write the behaviors that should happen  <!--meaning- you first--> 
        - then write the code that fulfills those <i>desires</i> 
- Supports a lot of languages, including **Java**, compatible with **JUnit assertions**, first class citizen in IDEA 
![bg right:50% 100%](desires.png)
---

# Why am I talking about this?
- e.g. used for functional and integration tests in stbactivation
- but, also for example in `id-oogway` 
    - Link to click for when you're checking out the slides: https://github.com/sky-uk/id-oogway/tree/master/component-test/src/test/resources


---
## Syntax
- Gherkin
- .feature files, tab indentation

---

#### Syntax (cont.)
* Basic syntax:
    * **Feature:** Name of the feature
        * **Scenario:** Name of the scenario
            * **Given X** (e.g. `Given the weather is hot`)
            * **When Y** (e.g. `When I ask you "is it hot outside?"`)
            * **Then A** (e.g. `Then I should be told "yeah it's time to hit the beach" by you`)

---
#### Syntax (cont.)
* **Scenario Outline**
    * Run the same Scenario multiple times, with different combinations of values (**Examples**)
* **Docstrings**
    * Docstring / multi-line comment (python doc-string syntax `"""bla"""`)
* **#** - Comments
* **@** - Tags
* Supports expressions - e.g.: `@When("I get {int} messages from the Kafka topic")`


# Syntax (last)
- Not exhaustive at all!
- More here: https://cucumber.io/docs/gherkin/reference/
- And here: https://github.com/cucumber/cucumber-expressions?tab=readme-ov-file#custom-parameter-types

- IntelliJ IDEA plugin available for .feature syntax <p class="small-text">(self-descriptive name "Gherkin")</span>
---

# Stop!
## Demo time! ⌛


# ![bg right:40% 80%](https://y.yarn.co/b0f94bf6-3db5-402e-9978-c45cb57eb094_text.gif)

**Sources / More material to read:**
<span class="small-text"> https://cucumber.io/docs/guides/10-minute-tutorial/?lang=java</span>
<span class="small-text"> https://cucumber.io/docs/gherkin/</span>
<span class="small-text">https://www.baeldung.com/java-cucumber-gradle</span>
<span class="small-text">https://github.com/cucumber/cucumber-expressions?tab=readme-ov-file</span>
<span class="small-text">https://cucumber.io/docs/gherkin/step-organization/?lang=java</span>