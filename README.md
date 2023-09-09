# Mergetest

This project is used to simulate the usage of multiple branches
to handle 3-way merges for mutilple delivery branches combined in
one main GitOps branch hosting multiple installations
fed by different delivery sources.

The goal is to feed in new updates for a set of delivery sources,
which will be used to setup and update multiple installation
configurations hosted in a single branch (main)

Whenever a new version for a delivery source is availble it might
bring a new version of the installation template initially used
to setup the installation configuration in the main branch.

This installation configuration is stored here under the folder
`installations/`&lt;name>. At these locations the local operator is
able to change installation settings.

Initially it is filled with a configuration template
provided by the software provider. This is then modified by
the operator to finalize the initial installation configuration
and later on to tweak the installtion of the software product.

Whenever a new version of this software product is delivered, it
might come with a new version of the installation template:

- with new required configuration parameters
- with changed default settings for existing parameters
- with hints for configuration changes required for the new version.

An upgrade is then proposed by a pull-request to the main branch.
Here, the new template versions must be merged with the modifications
done by the operator in the main branch for the installation
concered by the update. Hereby, the operator modification must be preserved
as far as possible.

Therefore the pull-request must carry the result of a 3-way kind of
merge for the configuration settings.

This can be achieved by using additional system-managed branches
for every installation exclusively hosting the sequence of version
updates for the delivery source.
An update then means:

- to add the new delivery version of the configuration template of a
  software product imported from the software provider to the appropriate
  delivery branch. This template also specified the product version
  to be deployed.
- this branch can then be used to create a (temporary) pull-request branch
  merging this delivery branch with the main branch content and committing
  all the merge conflict markers.
- by an additional special marker for required configuration changes a
  github check action can then vote on the PR to notify the operator of
  actions required to be done to finally finishing the update by merging
  the PR.
- the PR branch is then used by the operator to resolve the identified
  problems
- after a successful check the PR is finally merged into the main branch
  and the update process is completed after the GitOps environment
  has deployed the configuration changes found in the main branch.

To be able to do the described merges all involved branches must be based on 
the same initial commit. This is the one containing this description
and no more content.

A processing setting up a new installtion the looks as follows:

- setup a new delivery branch for the new installation with the
  initial commit.
- add the first configuration template from the actual version of the
  product to be installed imported from the software provider.
- create a (temporary) pull-request branch from the current version of
  the main branch and merge-in the new delivery branch.
- this merge should not provide any conflicts but the installation template
  may request the setting of required configuration parameters
  by use the marker described above.
- the check action will vote on the new PR and notify the operator
  on required actions.
- the opertator finishes the initial installation configuration
  by changing files in the the new installation folder, only.
- after a successful check the PR is finally merged into the main branch
  and the setup process is completed after the GitOps environment
  has deployed the new configuration now found in the main branch.

This process is identical to the update processm only the steps
preceeding are preceeded by the setup of the new delivery branch from the
initial base commit.
