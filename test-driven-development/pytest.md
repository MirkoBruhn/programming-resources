## Useful commands

`pytest -v --tb=line` one line per test, show the traceback

`pytest -xl` fail fast and show me everything

## Command line options

`v vebose`  show full diff

`test_name.py::test_func` run specific function

`-collect-only` doesn't run

`-k name` only runs tests matching name

`-m mark_name` runs marked tests 

`-x` exit on first fail

`-s` allows printing to STDOUT

`-l` prints out local vars if test fails

`-lf` run last failed
`-ff` run first failed

`-tb` modified the traceback - `short, line, no`
`--tb=no`

`-durations=N` shows runtime of tests

`-setup-show` shows fixtures used

## Marking test

Marked using `@pytest.mark.smoke`.

We can also mark tests with `skip`, `skipif` and `xfail` (expected to fail).

## Parametrizing tests

```python
@pytest.mark.parameterize('var', [list, of, vars, to, run])
def my_test_func(var):
    test_code(var)
```

Can also pass in multiple args
```python
@pytest.mark.parameterize(
    'var1', 'var2',
    [(var11, var21), (var21, var22)]
)
def my_test_(var1, var):
    test_code(var1, var2)
```

It is also possible to define the args to the `parameterize` decorator outside the decorator, but requires using ids to get print out (page 45).

## Fixtures

Run before/after tests (ie setup and teardown).

Use a `# GIVEN/WHEN/THEN` notation for tests with fixtures.

Use `conftest.py` to share fixtures between modules.

`tmpdir` is a built in fixture

```python
@pytest.fixture()
def my_fixture(tmpdir):

    #  setup
    make_database(tmpdir)

    #  run test
    yield

    #  teardown
    kill_database()
```

Args for fixtures:
- `autoreuse=True` means all tests will use the fixture
- `scope` controls how often the code runs.  Default is `func` (once per function run) - `session` to only run once per session