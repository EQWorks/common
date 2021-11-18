---
title: "Naming"
date: 2018-11-18T12:33:46+10:00
featured: true
weight: 1
---

# Naming

## End-to-end Consistency

Try to keep an end-to-end consistency, and preferably, back-to-front consistency, in our naming conventions.

This sometimes would go against common/community (non-enforcing) conventions. For instance, if SQL column names are in `underscore_connected_lowercases`, associated JavaScript Object key names should be kept as so (even if the applied JS style convention suggests `mixedCases`).

This consistency allows for an easier time on end-to-end communication, development and debugging. It makes code less error-prone, as no explicit case conversion are involved in the transport and business logic. And as a side benefit, all participants are naturally familiar with the data structure being passed over the wire.

Example:

```javascript
// some Node.js API server relaying PostgreSQL
router.get('/user/:first_name', (req, res, next) => {
  // 👍 GOOD -- direct extraction, no transformation
  const { first_name } = req.query
  // 👎 BAD -- wasteful transformation for "good" convention
  const firstName = req.query.first_name
  db.query({
    text: `
      SELECT
        id,
        first_name,
        last_name,
        role
      FROM user_table
      WHERE first_name = $1;
    `,
    values: [first_name],
  }).then(({ rows: [person] }) => {
    // 👍 GOOD -- direct relay, no transformation
    // data structure can be easily understood through ^SQL
    // as the "single origin of truth".
    return res.status(200).json(person)

    // 👎 BAD -- wasteful transformation for "good" convention
    // requires additional efforts to know what to expect from
    // this API endpoint.
    return res.status(200).json({
      id: person.id,
      firstName: person.first_name,
      // 👀 easily overlooked typo that cannot be caught at runtime
      lastNmae: person.last_name,
      role: person.role,
    })
  }).catch(next)
})

// cleaned up version with only 👍 GOOD parts
router.get('/user/:first_name', (req, res, next) => {
  const { first_name } = req.query
  db.query({
    text: `
      SELECT
        id,
        first_name,
        last_name,
        role
      FROM user_table
      WHERE first_name = $1;
    `,
    values: [first_name],
  }).then(({ rows: [person] }) => {
    return res.status(200).json(person)
  }).catch(next)
})
```

## Respect Common/Community Standard

Try to apply the commonly agreed naming standard by the given language/stack/framework's community. This saves us time from debating on coding styles and allows for an easier onboarding experience.

Some are more enforcing than others, such as Golang [attaches package interface visibility to naming rules](https://tour.golang.org/basics/3), while [Python's PEP8](https://www.python.org/dev/peps/pep-0008/#naming-conventions) and [Effective Go](https://golang.org/doc/effective_go.html#names) has recommended, but non-enforcing conventions.

Then there is JavaScript, [with](https://google.github.io/styleguide/jsguide.html) multiple [popular](https://github.com/airbnb/javascript) style [guides](https://standardjs.com/) that can be adopted/borrowed based on the common agreement between project maintainers.

## Respect Existing Conventions

Respect existing conventions applied in existing projects. Gradually revise upon common agreement between project maintainers, ideally toward an established common/community standard.

## Scope Dependent Naming

Prefer **comprehensive** and **concise** names for `classes`, `functions/methods`, and shared `variables` (such as constants, globals).

Prefer **short** but **relevant** names for locally scoped `variables` and `functions` provided no conflict within the same scope, and the scope does not entail lengthy code. This is borrowed from the real-life convention of signing documents -- often there is only one signature required per-page (or even per-document), but any "local" (significant fields) acknowledgments are in the form of initials.

Python example:

```python
import os

# module constants/globals
PROD_SQL_URL = os.getenv('SQL_URL')

# classes
class PreAggregationPipeline:

    # functions
    def write_into_db(self, rows=None):

        # closure/enclosed local functions
        def proc(row):
            # some logic to process row
            return new_row

        # local variables
        for r in rows:
            # close context - `r` = row, `nr` = new row
            nr = proc(r)
```

Golang example:

```golang
// package constant/globals/structs
type Maintenance struct {
    Message string `json:"message,omitempty"`
    Start   int    `json:"start"`
    End     int    `json:"end,omitempty"`
    Service string `json:"service"`
    Remove  bool   `json:",omitempty"`
}

// functions, struct methods (public)
func (maint Maintenance) MakeMap() map[string]interface{} {
    // local variables
    m := map[string]interface{}{
        "service": maint.Service,
        "start":   maint.Start,
    }
    end := maint.End
    if end != 0 {
        m["end"] = end
    }
    if maint.Message != "" {
        m["message"] = maint.Message
    }
    return m
}

// functions (private, or special case such as main)
func main() {

}
```

JavaScript example:

```javascript
// classes
function WonderfulPerson(data) {
  this.firstName = data.firstName
  this.lastName = data.lastName
}

// methods/functions
WonderfulPerson.prototype.toString = () => {
  // closure/locally scoped functions/variables
  const cap = s => s.charAt(0).toUpperCase() + s.slice(1)

  return `${cap(this.lastName)} ${cap(this.firstName)}`
}
```

## Code and Files Associative Naming

Keep a consistent association between code and its containing files and folders (directories).

Prefer lowercase naming convention for file/folder names, because while the filesystems of Linux are case sensitive, **macOS** and Windows aren't.

Prefer `dash-connected` naming convention, because [`-` (dash) is a better delimiter than `' '` (space) and `_` (underscore)](https://blog.codinghorror.com/of-spaces-underscores-and-dashes/).

Examples:

Golang example:

```golang
// types/maintenance/main.go
package maintenance

type Maintenance struct {
    Message string `json:"message,omitempty"`
    Start   int    `json:"start"`
    End     int    `json:"end,omitempty"`
    Service string `json:"service"`
    Remove  bool   `json:",omitempty"`
}

// which is imported in other packages as
import "<module>/types/maintenance"
```

JavaScript example:

```jsx
// connection-hub/index.js
export const ConnectionHub = (props) => (
  <Connections {...props} />
)
```

Python example:

```python
# pre-aggregation-pipeline.py
def pre_aggregation_pipeline():
    pass
```
