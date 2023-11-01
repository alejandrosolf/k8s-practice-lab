# Daemonsets

**To check tasks and get secret phrases run:**

    $ ./checker -course 'kubernetes' -course-version 'daemonsets' -test-suite 'daemonset'

**NOTE:** before running check after each task make sure that daemonset or nodes are up and running.

**Task 1:**

Create a new node and set up `worker` role for it.

**Do not forget to copy secret phrase, test will fail after task 5.**

**Task 2:**

Taint your nodes.

    Requirements:
    control-plane:
    key: node-role.kubernetes.io/control-plane
    effect: NoSchedule
    worker:
    key: node-role.kubernetes.io/worker
    effect: NoSchedule

**Do not forget to copy secret phrase, test will fail after task 6.**

**Task 3:**

Deploy daemonset

    Requirements:
    Name: fluentd-elasticsearch
    Image: quay.io/fluentd_elasticsearch/fluentd:v2.5.2

_Please pay attention how many pods were created and why._

**Do not forget to copy secret phrase, test will fail after next task.**

**Task 4:**

Modify `fluentd-elasticsearch` DaemonSet to ensure that pods run on every node.**You should change only DaemonSet configuration!**

**Do not forget to copy secret phrase, test will fail after next task.**

**Task 5:**

Create one more node and set up `worker` role for it.

_Please pay attention on number of pods._

**Do not forget to copy secret phrase, test will fail after task 6.**

**Task 6:**

**jq utility should be installed before running checker!**

*   Get details of nodes in JSON format and save it to `$HOME/nodes-info.json` file.
*   Delete all `worker` nodes.
*   Untaint `control-plane` node.
*   Remove `fluentd-elasticsearch` DaemonSet.

This is it with DaemonSets.