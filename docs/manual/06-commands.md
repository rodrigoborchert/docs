# Commands

A _command_ is a single executable string executed on a Node.
Rundeck invokes commands on nodes via a _node executor_
which evaluates the command string and executes it.
Node executors evaluate the command string in a data context
containing information about the Node resource. Command strings
can reference this data and thus avoid hard coding node or environment
specific values.

The Rundeck graphical console provides the ability to execute
commands to a set of filtered Node resources.
The Command page can accept any command string you might run
via an SSH command or via the [rd adhoc](https://rundeck.github.io/rundeck-cli/commands/#adhoc) shell tool.

::: tip
Your ability to view Nodes and execute commands on them
depends on your ACL policy.
:::

## Commands tab overview

Navigate to this page by clicking on the "Commands" tab in the navigation
bar. Alternatively, go to the Nodes tab and choose the "Node Actions" menu
and select the "Run a command ..." menu item.

![Ad-hoc Command](~@assets/img/command-overview.png)

The screenshot above shows the elements of the Commands page user interface.

1. Filter expression - Search expression to match nodes.
2. Filter results list - Matching nodes presented as a list here.
3. Choose the Targer Runner - Select by Tag or Tags.
4. Command prompt - Enter the command string.
5. Command dispatch settings - Optional settings to control concurrency and errors.
6. Run command button - Execute command for command string and matched nodes.
7. Activity views - Historical views of command executions.


## Selecting a Runner

:::tip New Feature
Note: This feature is only available after version 4.11 of Process Automation with the new Distributed Automation flag turned on.  [More info](/administration/runner/runner-intro.md).
:::

Selecting the Runner here will dispatch the commands to an Enterprise Runner instance.

## Enter a command

![Input command string](~@assets/img/fig0207-a.png)

Enter the command string you wish to execute on the Nodes. This command
string must be a valid command statement that can be executed on the nodes.

### Dispatch settings

![Choose dispatch settings](~@assets/img/fig0208-b.png "Foo")

The dispatch settings let you control the amount of concurrency and error
handling for the command execution.

- Thread count: Number of concurrent command executions. By default the value is 1 which causes a sequential execution.
- On node failure: If a command execution fails on the node, you can choose to continue (default) or stop immediately at the failed node.

## Select the nodes

![Filter the nodes](~@assets/img/fig0207-b.png)

You can choose the nodes by either choosing a saved filter or typing in your own
filter expression. Press the "Search" button to find the matched nodes.
You can get help on filter expression syntax by pressing the help button.

### Node detail

Each of the matched nodes is linked to a detail view where you can inspect
the Node's attribute values (1).

You can click the filter links inside the detail
view to continue building your filter expression (2).

![Node detail](~@assets/img/fig0208-a.png)

## Execute command

With the command string and filter entered you are ready to run the command.
Press the "Run on x Nodes" button to begin the execution.

The command will be
dispatched to all the Nodes matched by the filter.
The command prompt and run button become disabled until
the execution completes. Output from the command execution is shown
below.

![Command execution output](~@assets/img/fig0208.png)

1. Link to execution page: Every execution has an ID an a separate page to follow it and view a report after it completes.
2. Collated output: All output is grouped by the node.
3. You can dismiss the output by pressing the "X" button next to the
   command's status.

## Monitor the execution

Once the command execution begins you can monitor its progress on the
Commands page or a separate execution follow page discussed later.

![Now running a command](~@assets/img/fig0207-c.png)

1. Kill job button: You can kill the execution by pressing this button.

### Execution follow page

Sometimes it is useful to have a page where just the execution output
is displayed separately. One purpose is to share a link to others
interested in following the output messages. Click on the execution id go to the execution follow page.

![Click execution id to follow the execution](~@assets/img/fig0207-f.png)

![Execution follow view](~@assets/img/fig0207-d.png)

Notice the URL in the location bar of your browser. This URL can
be shared to others interested in the progress of execution. The URL
contains the execution ID (EID) and has a form like:

     http://rundeckserver/project/prod/execution/show/{EID}

After execution completes, the command will have a status:

- Successful: No errors occurred during execution of the command
  across the filtered Node set
- Failed: One or more errors occurred. A list of Nodes that incurred
  an error is displayed. The page will also contain a link "Retry
  Failed Nodes..." in case you would like to retry the command.

## Related Command line tools

[rd adhoc](https://rundeck.github.io/rundeck-cli/commands/#adhoc)
~ Execute ad hoc commands and scripts to matching nodes.

[rd executions](https://rundeck.github.io/rundeck-cli/commands/#executions)
~ List running executions, attach and follow their output, or kill them.
