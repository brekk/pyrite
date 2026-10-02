# pyrite

golden / snapshot tests in `madlib`

[![Madlib Project Badge](https://img.shields.io/badge/madlib-purple?logo=github&logoSize=auto)](//github.com/madlib-lang/madlib) <!-- $MADLIB.projectBadge -->
[![pyrite v0.0.1](https://img.shields.io/badge/v0.0.1-purple?label=version)](//github.com/brekk/pyrite) <!-- $MADLIB.json.version -->

---

If you have something which produces a serializable output, sometimes you want to be able to take a snapshot of that output and later, compare it to new output to see if things have changed. This gives you a convenient way of demarcating when basic expectations have changed in a simple way.

Pyrite allows you to create these snapshots, using very little markup:

```madlib
import Pyrite from "Pyrite"
import Snapshot from "Pyrite/Snapshot"

serialize = () => "saved!"

snapshotter = Pyrite.createRecorder("./golden")
Snapshot.testSnapshot(snapshotter(serialize, "record of note"))
```

This basically tells Pyrite to create a new file store in `./golden`, and to create a `record of note` file (currently slugged and turned into `record-of-note.golden.txt`) with the body of that file `saved!`. We can add this `./golden` folder to our version control (recommended!) and continue developing.

Later on, we can compare `testSnapshot` calls with the written value in the old `./golden/record-of-note.golden.txt` with the new `serialize` function's output. If they don't match, it will fail the test, which will give us an immediate indication of change.
