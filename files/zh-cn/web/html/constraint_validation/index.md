---
title: 约束验证
slug: Web/HTML/Constraint_validation
original_slug: Web/Guide/HTML/Constraint_validation
---

创建 web 表单始终是一个复杂的任务。仅仅组装表单是容易的，但是检查每一个字段的值是否有效并且一致是一件更加困难的事情，而向用户指明错误可能会令人头痛。[HTML5](/zh-CN/docs/Web/Guide/HTML/HTML5) 引入了表单相关的一些新的机制：为{{ HTMLElement("input") }}元素和强制校验增加了一些新的语义类型，使得在客户端检查表单内容的工作变得容易。基本上，在填写字段时，通常这些约束都会被检查，而不需要额外的 JavaScript 代码进行校验； 对于更复杂的约束条件的校验可以尝试使用 HTML5 [Constraint Validation API](/zh-CN/docs/Web/Guide/HTML/Forms_in_HTML#Constraint_Validation_API).

> **备注：** HTML5 Constraint validation doesn't remove the need for validation on the _server side_. Even though far fewer invalid form requests are to be expected, invalid ones can still be sent by non-compliant browsers (for instance, browsers without HTML5 and without JavaScript) or by bad guys trying to trick your web application. Therefore, like with HTML4, you need to also validate input constraints on the server side, in a way that is consistent with what is done on the client side.

## 固有和基本的约束

在 HTML5 中，声明基本的约束有两种方式：

- 给 {{ HTMLElement("input") }} 元素的 {{ htmlattrxref("type", "input") }} 特性选择最合适的语义化的值，比如，选择 email 类型将会自动创建一个约束用于检查输入的值是否是一个有效的 e-mail 地址。
- 设置验证相关的特性值，允许用一种简单的方式来描述基本的约束，而不必要使用 JavaScript。

### 语义的 input 类型

{{ htmlattrxref("type", "input") }} 特性中固有约束：

<table class="no-markdown">
  <thead>
    <tr>
      <th scope="col">Input 类型</th>
      <th scope="col">约束描述</th>
      <th scope="col">Associated violation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&#x3C;input type="URL"></td>
      <td>
        值必须是绝对的 URL，即，是下面的某一种：
        <ul>
          <li>
            a valid URI (as defined in
            <a href="http://www.ietf.org/rfc/rfc3986.txt">RFC 3986</a>)
          </li>
          <li>
            a valid IRI, without a query component (as defined in
            <a href="http://www.ietf.org/rfc/rfc3987.txt">RFC 3987</a>)
          </li>
          <li>
            a valid IRI, with a query component without any unescaped non-ASCII
            character (as defined in
            <a href="http://www.ietf.org/rfc/rfc3987.txt">RFC 3987</a>)
          </li>
          <li>
            a valid IRI, and the character set for the document is UTF-8 or
            UTF-16 (as defined in
            <a href="http://www.ietf.org/rfc/rfc3987.txt">RFC 3987</a>)
          </li>
        </ul>
      </td>
      <td><strong>Type mismatch </strong>constraint violation</td>
    </tr>
    <tr>
      <td>&#x3C;input type="email"></td>
      <td>
        The value must follow the
        <a href="http://www.ietf.org/rfc/std/std68.txt">ABNF</a> production:
        <code>1*( atext / "." ) "@" ldh-str 1*( "." ldh-str )</code> where:
        <ul>
          <li>
            <code>atext</code> is defined in
            <a href="http://tools.ietf.org/html/rfc5322">RFC 5322</a>, i.e., a
            US-ASCII letter (A to Z and a-z), a digit (0 to 9) or one of the
            following! # $ % &#x26; ' * + - / = ? ` { } | ~ special character,
          </li>
          <li>
            <code>ldh-str</code> is defined in
            <a href="http://www.apps.ietf.org/rfc/rfc1034.html#sec-3.5"
              >RFC 1034</a
            >, i.e., US-ASCII letters, mixed with digits and - grouped in words
            separated by a dot (.).
          </li>
        </ul>
        <div class="note">
          <strong>Note:</strong> if the
          {{ htmlattrxref("multiple", "input") }} attribute is set,
          several e-mail addresses can be set, as a comma-separated list, for
          this input. If any of these do not satisfy the condition described
          here, the <strong>Type mismatch </strong>constraint violation is
          triggered.
        </div>
      </td>
      <td><strong>Type mismatch </strong>constraint violation</td>
    </tr>
  </tbody>
</table>

Note that most input types don't have intrinsic constraints, as some are simply barred from constraint validation or have a sanitization algorithm transforming incorrect values to a correct default.

### 验证相关的特性（Attribute）

下列特性用于描述基本的约束：

<table class="no-markdown">
  <thead>
    <tr>
      <th scope="col">特性</th>
      <th scope="col">支持该特性的 Input 类型</th>
      <th scope="col">可接受的值</th>
      <th scope="col">约束描述</th>
      <th scope="col">Associated violation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>{{ htmlattrxref("pattern", "input") }}</td>
      <td>text, search, url, tel, email, password</td>
      <td>
        A
        <a href="/en-US/docs/Web/JavaScript/Guide/Regular_Expressions"
          >JavaScript regular expression</a
        >
        (compiled with the
        <a
          href="http://www.ecma-international.org/publications/standards/Ecma-262.htm"
          >ECMAScript 5</a
        >
        <code title="">global</code>, <code title="">ignoreCase</code>, and
        <code title="">multiline</code> flags <em>disabled)</em>
      </td>
      <td>输入的值必须匹配设置的模式。</td>
      <td><strong>Pattern mismatch</strong> constraint violation</td>
    </tr>
    <tr>
      <td rowspan="3">{{ htmlattrxref("min", "input") }}</td>
      <td>range, number</td>
      <td>A valid number</td>
      <td rowspan="3">输入的值必须大于等于设置的最小值。</td>
      <td rowspan="3"><strong>Underflow</strong> constraint violation</td>
    </tr>
    <tr>
      <td>date, month, week</td>
      <td>A valid date</td>
    </tr>
    <tr>
      <td>datetime, datetime-local, time</td>
      <td>A valid date and time</td>
    </tr>
    <tr>
      <td rowspan="3">{{ htmlattrxref("max", "input") }}</td>
      <td>range, number</td>
      <td>A valid number</td>
      <td rowspan="3">输入的值必须小于等于设置的最大值。</td>
      <td rowspan="3"><strong>Overflow</strong> constraint violation</td>
    </tr>
    <tr>
      <td>date, month, week</td>
      <td>A valid date</td>
    </tr>
    <tr>
      <td>datetime, datetime-local, time</td>
      <td>A valid date and time</td>
    </tr>
    <tr>
      <td>{{ htmlattrxref("required", "input") }}</td>
      <td>
        text, search, url, tel, email, password, date, datetime, datetime-local,
        month, week, time, number, checkbox, radio, file; also on the
        {{ HTMLElement("select") }} and
        {{ HTMLElement("textarea") }} elements
      </td>
      <td>
        <em>none</em> as it is a Boolean attribute: its presence means
        <em>true</em>, its absence means <em>false</em>
      </td>
      <td>There must be a value (if set).</td>
      <td><strong>Missing</strong> constraint violation</td>
    </tr>
    <tr>
      <td rowspan="5">{{ htmlattrxref("step", "input") }}</td>
      <td>date</td>
      <td>An integer number of days</td>
      <td rowspan="5">
        Unless the step is set to the any literal, the value must be
        <strong>min</strong> + an integral multiple of the step.
      </td>
      <td rowspan="5"><strong>Step mismatch </strong>constraint violation</td>
    </tr>
    <tr>
      <td>month</td>
      <td>An integer number of months</td>
    </tr>
    <tr>
      <td>week</td>
      <td>An integer number of weeks</td>
    </tr>
    <tr>
      <td>datetime, datetime-local, time</td>
      <td>An integer number of seconds</td>
    </tr>
    <tr>
      <td>range, number</td>
      <td>An integer</td>
    </tr>
    <tr>
      <td>{{ htmlattrxref("maxlength", "input") }}</td>
      <td>
        text, search, url, tel, email, password; also on the
        {{ HTMLElement("textarea") }} element
      </td>
      <td>An integer length</td>
      <td>
        The number of characters (code points) must not exceed the value of the
        attribute.
      </td>
      <td><strong>Too long</strong> constraint violation</td>
    </tr>
  </tbody>
</table>

## Constraint validation process

Constraint validation is done through the Constraint Validation API either on a single form element or at the form level, on the {{ HTMLElement("form") }} element itself. The constraint validation is done in the following ways:

- By a call to the checkValidity() method of a form-related [DOM](/zh-CN/docs/DOM) interface ([`HTMLInputElement`](/en-US/docs/Web/API/HTMLInputElement), [`HTMLSelectElement`](/en-US/docs/Web/API/HTMLSelectElement), [`HTMLButtonElement`](/en-US/docs/Web/API/HTMLButtonElement) or [`HTMLTextAreaElement`](/en-US/docs/Web/API/HTMLTextAreaElement)), which evaluates the constraints only on this element, allowing a script to get this information. (This is typically done by the user-agent when determining which of the [CSS](/zh-CN/docs/Web/CSS) pseudo-classes, {{ Cssxref(":valid") }} or {{ Cssxref(":invalid") }}, applies.)
- By a call to the checkValidity() function on the [`HTMLFormElement`](/en-US/docs/Web/API/HTMLFormElement) interface, which is called _statically validating the constraints_.
- By submitting the form itself, which is called _interactively validating the constraints_.

> **备注：**
>
> - If the {{ htmlattrxref("novalidate", "form") }} attribute is set on the {{ HTMLElement("form") }} element, interactive validation of the constraints doesn't happen.
> - Calling the send() method on the [HTMLFormElement](/en/DOM/HTMLFormElement) interface doesn't trigger a constraint validation. In other words, this method sends the form data to the server even if doesn't satisfy the constraints.

## Complex constraints using HTML5 Constraint API

Using JavaScript and the Constraint API, it is possible to implement more complex constraints, for example, constraints combining several fields, or constraints involving complex calculations.

Basically, the idea is to trigger JavaScript on some form field event (like **onchange**) to calculate whether the constraint is violated, and then to use the method `field.setCustomValidity()` to set the result of the validation: an empty string means the constraint is satisfied, and any other string means there is an error and this string is the error message to display to the user.

### Constraint combining several fields: Postal code validation

The postal code format varies from one country to another. Not only do most countries allow an optional prefix with the country code (like `D-` in Germany, `F-` in France or Switzerland), but some countries have postal codes with only a fixed number of digits; others, like the UK, have more complex structures, allowing letters at some specific positions.

> **备注：**This is not a comprehensive postal code validation library, but rather a demonstration of the key concepts.

As an example, we will add a script checking the constraint validation for this simple form:

```html
<form>
    <label for="ZIP">ZIP : </label>
    <input type="text" id="ZIP">
    <label for="Country">Country : </label>
    <select id="Country">
      <option value="ch">Switzerland</option>
      <option value="fr">France</option>
      <option value="de">Germany</option>
      <option value="nl">The Netherlands</option>
    </select>
    <input type="submit" value="Validate">
</form>
```

This displays the following form:

{{EmbedLiveSample("Constraint combining several fields: Postal code validation")}}

First, we write a function checking the constraint itself:

```js
function checkZIP() {
  // For each country, defines the pattern that the ZIP has to follow
  var constraints = {
    ch : [ '^(CH-)?\\d{4}$', "Switzerland ZIPs must have exactly 4 digits: e.g. CH-1950 or 1950" ],
    fr : [ '^(F-)?\\d{5}$' , "France ZIPs must have exactly 5 digits: e.g. F-75012 or 75012" ],
    de : [ '^(D-)?\\d{5}$' , "Germany ZIPs must have exactly 5 digits: e.g. D-12345 or 12345" ],
    nl : [ '^(NL-)?\\d{4}\\s*([A-RT-Z][A-Z]|S[BCE-RT-Z])$',
                    "Nederland ZIPs must have exactly 4 digits, followed by 2 letters except SA, SD and SS" ]
  };

  // Read the country id
  var country = document.getElementById("Country").value;

  // Get the NPA field
  var ZIPField = document.getElementById("ZIP");

  // Build the constraint checker
  var constraint = new RegExp(constraints[country][0], "");
    console.log(constraint);


  // Check it!
  if (constraint.test(ZIPField.value)) {
    // The ZIP follows the constraint, we use the ConstraintAPI to tell it
    ZIPField.setCustomValidity("");
  }
  else {
    // The ZIP doesn't follow the constraint, we use the ConstraintAPI to
    // give a message about the format required for this country
    ZIPField.setCustomValidity(constraints[country][1]);
  }
}
```

Then we link it to the **onchange** event for the {{ HTMLElement("select") }} and the **oninput** event for the {{ HTMLElement("input") }}:

```js
window.onload = function () {
    document.getElementById("Country").onchange = checkZIP;
    document.getElementById("ZIP").oninput = checkZIP;
}
```

You can see a [live example](/@api/deki/files/4744/=constraint.html) of the postal code validation.

### Limiting the size of a file before its upload

Another common constraint is to limit the size of a file to be uploaded. Checking this on the client side before the file is transmitted to the server requires combining the Constraint API, and especially the field.setCustomValidity() method, with another JavaScript API, here the HTML5 File API.

Here is the HTML part:

```html
<label for="FS">Select a file smaller than 75 kB : </label>
<input type="file" id="FS">
```

This displays:

{{EmbedLiveSample("Limiting the size of a file before its upload")}}

The JavaScript reads the file selected, uses the File.size() method to get its size, compares it to the (hard coded) limit, and calls the Constraint API to inform the browser if there is a violation:

```js
function checkFileSize() {
  var FS = document.getElementById("FS");
  var files = FS.files;

  // If there is (at least) one file selected
  if (files.length > 0) {
     if (files[0].size > 75 * 1024) { // Check the constraint
       FS.setCustomValidity("The selected file must not be larger than 75 kB");
       return;
     }
  }
  // No custom constraint violation
  FS.setCustomValidity("");
}
```

Finally we hook the method with the correct event:

```js
window.onload = function () {
  document.getElementById("FS").onchange = checkFileSize;
}
```

You can see a [live example](/@api/deki/files/4745/=fileconstraint.html) of the File size constraint validation.

## Visual styling of constraint validation

Apart from setting constraints, web developers want to control what messages are displayed to the users and how they are styled.

### Controlling the look of elements

The look of elements can be controlled via CSS pseudo-classes.

#### :required and :optional CSS pseudo-classes

The [`:required`](/zh-CN/docs/Web/CSS/:required) and [`:optional`](/zh-CN/docs/Web/CSS/:optional) [pseudo-classes](/zh-CN/docs/Web/CSS/Pseudo-classes) allow writing selectors that match form elements that have the {{ htmlattrxref("required") }} attribute, or that don't have it.

#### :-moz-placeholder CSS pseudo-class

See [:-moz-placeholder](/zh-CN/docs/Web/CSS/:-moz-placeholder).

#### :valid :invalid CSS pseudo-classes

The [:valid](/zh-CN/docs/Web/CSS/:valid) and [:invalid](/zh-CN/docs/Web/CSS/:invalid) [pseudo-classes](/zh-CN/docs/Web/CSS/Pseudo-classes) are used to represent \<input> elements whose content validates and fails to validate respectively according to the input's type setting. These classes allow the user to style valid or invalid form elements to make it easier to identify elements that are either formatted correctly or incorrectly.

#### Default styles

### Controlling the text of constraints violation

#### The x-moz-errormessage attribute

The x-moz-errormessage attribute is a Mozilla extension that allows you to specify the error message to display when a field does not successfully validate.

> **备注：** Note: This extension is non-standard.

#### Constraint API's element.setCustomValidity()

The element.setCustomValidity(error) method is used to set a custom error message to be displayed when a form is submitted. The method works by taking a string parameter error. If error is a non-empty string, the method assumes validation was unsuccessful and displays error as an error message. If error is an empty string, the element is considered validated and resets the error message.

#### Constraint API's ValidityState object

The DOM [`ValidityState`](/zh-CN/docs/Web/API/ValidityState) interface represents the _validity states_ that an element can be in, with respect to constraint validation. Together, they help explain why an element's value fails to validate, if it's not valid.

### Examples of personalized styling

### HTML4 fallback

#### Trivial fallback

#### JS fallback

## Conclusion
