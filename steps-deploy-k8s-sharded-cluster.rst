.. procedure::
   :style: normal

.. step: Configure ``kubectl`` to default to your namespace.


If you have not already, run the following command to execute all 
``kubectl`` commands in the namespace you :ref:`created <k8s-prerequisites>`.

.. note::

    .. include:: /includes/admonitions/note-om-context-scope-multi-cluster.rst

.. code-block:: sh

   kubectl config set-context $(kubectl config current-context) --namespace=<metadata.namespace>

.. step: Copy the sample :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` resource.


Change the settings of this |yaml| file to match your
desired :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` configuration.


This is a |yaml| file that you can modify to meet your desired
configuration. Change the settings to match your desired
:manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` configuration.

.. literalinclude:: /includes/code-examples/yaml-files/example-sharded-cluster.yaml
   :language: yaml
   :start-after: START-regular-sharded
   :end-before: END-regular-sharded
   :linenos:


.. step: Paste the copied example to create a new :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` resource.

Open your preferred text editor and paste the |k8s-obj| specification
into a new text file.

.. step Configure the settings highlighted in the preceding step as follows.


.. list-table::
   :widths: 10 20 50 20
   :header-rows: 1

   * - Key
     - Type
     - Description
     - Example

   * - :setting:`metadata.name`
     - string
     - Label for this |k8s| :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` |k8s-obj|.

       .. include:: /includes/fact-resource-name-char-limit.rst

       .. seealso::

          - :setting:`metadata.name`
          - |k8s| documentation on :k8sdocs:`names </concepts/overview/working-with-objects/names/>`.

     - ``myproject``

   * - :setting:`spec.shardCount`
     - integer
     - Number of shards to deploy.
     - ``2``

   * - :setting:`spec.mongodsPerShardCount`
     - integer
     - Number of shard members per shard.
     - ``3``

   * - :setting:`spec.mongosCount`
     - integer
     - Number of shard routers to deploy.
     - ``2``

   * - :setting:`spec.configServerCount`
     - integer
     - Number of members of the config server replica set.
     - ``3``

   * - :setting:`spec.version`
     - string
     - Version of MongoDB that this :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` should run.

       The format should be ``X.Y.Z`` for the Community edition and
       ``X.Y.Z-ent`` for the Enterprise edition.

       .. include:: /includes/admonitions/ubi-8-min-db-versions.rst

       To learn more about MongoDB versioning, see
       :ref:`release-version-numbers` in the MongoDB Manual.
     - .. include:: /includes/facts/fact-which-appdb-version.rst

   * - :setting:`spec.opsManager.configMapRef.name`
     - string
     - Name of the |k8s-configmap| with the |onprem| connection
       configuration. The
       :setting:`spec.cloudManager.configMapRef.name` setting is an
       alias for this setting and can be used in its place.

       .. include:: /includes/admonitions/note-namespace-match-configmap.rst

       .. include:: /includes/admonitions/fact-k8s-operator-manages-configmap.rst

     - ``<myproject>``

   * - :setting:`spec.credentials`
     - string
     - Name of the secret you
       :ref:`created <create-k8s-secret>` as |mms| |api|
       authentication credentials for the |k8s-op-short| to
       communicate with |onprem|.

       .. include:: /includes/admonitions/note-namespace-match-secret.rst

       .. include:: /includes/admonitions/fact-k8s-operator-manages-secret.rst

     - ``<mycredentials>``

   * - :setting:`spec.type`
     - string
     - Type of |k8s-mdbrsc| to create.

     - ``ShardedCluster``

   * - :setting:`spec.persistent`
     - string
     - *Optional.*

       Flag indicating if this |k8s-mdbrsc| should use |k8s-pvs| for
       storage. Persistent volumes are not deleted when the
       |k8s-mdbrsc| is stopped or restarted.

       If this value is ``true``, then the following values are set
       to their default value of ``16Gi``:

       - :setting:`spec.shardPodSpec.persistence.single`
       - :setting:`spec.configSrvPodSpec.persistence.single`

       To change your |k8s-pvcs| configuration, configure the
       following collections to meet your deployment requirements:

       - If you want one |k8s-pv| for each |k8s-pod|, configure the
         :setting:`spec.shardPodSpec.persistence.single` and
         :setting:`spec.configSrvPodSpec.persistence.single`
         collections.

       - If you want separate |k8s-pvs| for data, journals, and
         logs for each |k8s-pod|, configure the following
         collections:

         - In the ``spec.configSrvPodSpec.persistence.multiple``
           collection:
           - :setting:`.data <spec.configSrvPodSpec.persistence.multiple.data>`
           - :setting:`.journal <spec.configSrvPodSpec.persistence.multiple.journal>`
           - :setting:`.logs <spec.configSrvPodSpec.persistence.multiple.logs>`

         - In the ``spec.configSrvPodSpec.persistence.multiple`` collection:
           - :setting:`.data <spec.shardPodSpec.persistence.multiple.data>`
           - :setting:`.journal <spec.shardPodSpec.persistence.multiple.journal>`
           - :setting:`.logs <spec.shardPodSpec.persistence.multiple.logs>`

       .. include:: /includes/admonitions/k8s-persistent-volumes.rst

     - ``true``

.. step: Add any additional accepted settings for a :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` deployment.

You can also add any of the following optional settings to the
|k8s-obj| specification file for a :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>`
deployment:

- :setting:`spec.backup.assignmentLabels`
- :setting:`spec.backup.mode`
- :setting:`spec.backup.snapshotSchedule.snapshotIntervalHours`
- :setting:`spec.backup.snapshotSchedule.snapshotRetentionDays`
- :setting:`spec.backup.snapshotSchedule.dailySnapshotRetentionDays`
- :setting:`spec.backup.snapshotSchedule.weeklySnapshotRetentionWeeks`
- :setting:`spec.backup.snapshotSchedule.monthlySnapshotRetentionMonths`
- :setting:`spec.backup.snapshotSchedule.pointInTimeWindowHours`
- :setting:`spec.backup.snapshotSchedule.referenceHourOfDay`
- :setting:`spec.backup.snapshotSchedule.referenceMinuteOfHour`
- :setting:`spec.backup.snapshotSchedule.fullIncrementalDayOfWeek`
- :setting:`spec.backup.snapshotSchedule.clusterCheckpointIntervalMin`
- :setting:`spec.clusterDomain`
- :setting:`spec.connectivity.replicaSetHorizons`
- :setting:`spec.featureCompatibilityVersion`
- :setting:`spec.logLevel`

.. include:: /includes/admonitions/warning-set-cluster-name.rst

**For config server**

- :setting:`spec.configSrv.additionalMongodConfig`
- :setting:`spec.configSrvPodSpec.persistence.single`
- :setting:`spec.configSrvPodSpec.persistence.multiple.data`
- :setting:`spec.configSrvPodSpec.persistence.multiple.journal`
- :setting:`spec.configSrvPodSpec.persistence.multiple.logs`
- :setting:`spec.configSrvPodSpec.podTemplate.affinity.podAffinity`
- :setting:`spec.configSrvPodSpec.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution.topologyKey`
- :setting:`spec.configSrvPodSpec.podTemplate.affinity.nodeAffinity`
- :setting:`spec.configSrvPodSpec.podTemplate.metadata`
- :setting:`spec.configSrvPodSpec.podTemplate.spec`

**For shard routers**

- :setting:`spec.mongos.additionalMongodConfig`
- :setting:`spec.mongosPodSpec.podTemplate.affinity.podAffinity`
- :setting:`spec.mongosPodSpec.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution.topologyKey`
- :setting:`spec.mongosPodSpec.podTemplate.affinity.nodeAffinity`
- :setting:`spec.mongosPodSpec.podTemplate.metadata`
- :setting:`spec.mongosPodSpec.podTemplate.spec`

**For shard members**

- :setting:`spec.shard.additionalMongodConfig`
- :setting:`spec.shardPodSpec.persistence.single`
- :setting:`spec.shardPodSpec.persistence.multiple.data`
- :setting:`spec.shardPodSpec.persistence.multiple.journal`
- :setting:`spec.shardPodSpec.persistence.multiple.logs`
- :setting:`spec.shardPodSpec.podTemplate.affinity.podAffinity`
- :setting:`spec.shardPodSpec.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution.topologyKey`
- :setting:`spec.shardPodSpec.podTemplate.affinity.nodeAffinity`
- :setting:`spec.shardPodSpec.podTemplate.metadata`
- :setting:`spec.shardPodSpec.podTemplate.spec`
- :setting:`spec.shardSpecificPodSpec`

.. step Save this file with a ``.yaml`` file extension.

.. step Start your :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` deployment.


Invoke the following |k8s| command to create your
:manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>`:

.. code-block:: sh

   kubectl apply -f <sharded-cluster-conf>.yaml

:ref:`Check the log <k8s-troubleshooting>` after running this
command. If the creation was successful, you should see a message
similar to the following:

.. code-block:: sh

   2018-06-26T10:30:30.346Z INFO operator/shardedclusterkube.go:52 Created! {"sharded cluster": "my-sharded-cluster"}

.. step Track the status of your :manual:`sharded cluster </reference/glossary/#std-term-sharded-cluster>` deployment.


.. include:: /includes/check-resource-status.rst

