.. procedure::
   :style: normal
      
   .. step Update to the latest version of the `MongoDB Helm Charts for Kubernetes <https://mongodb.github.io/helm-charts>`__.
      
      .. code-block:: sh
      
         helm repo update mongodb https://mongodb.github.io/helm-charts
      
   .. step: If you are upgrading the Operator to version 1.13.0 or later, specify the :setting:`spec.opsManager.configMapRef.name` or the :setting:`spec.cloudManager.configMapRef.name` settings:
      
      1. Open the :ref:`k8s-specification` in the editor of your choice.
      #. Add the value to the :setting:`spec.opsManager.configMapRef.name`
         setting or the
         :setting:`spec.cloudManager.configMapRef.name` setting and save
         the specification.
      
      To learn more, see :ref:`Changes to the MongoDB Resource <ent_op-1.13.0-mdb-resource>`.
      
   .. step: Customize your Helm Chart before upgrading it.
      
      To learn about optional |k8s-op-short| installation settings, see
      :ref:`Operator Helm Installation Settings <meko-op-install-settings-helm>`.
      
   .. step: Upgrade the |k8s-op-short|.
      
      Invoke the following ``helm`` command:
      
      .. code-block:: sh
      
         helm upgrade enterprise-operator mongodb/enterprise-operator
      
