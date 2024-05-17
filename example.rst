.. procedure::
   :style: normal
      
      
   .. step:: Update to the latest version of the `MongoDB Helm Charts for Kubernetes <https://mongodb.github.io/helm-charts>`__.
      
      Run the following command to check the version of your current Helm template:
      
      .. code-block:: sh
      
         helm search repo mongodb/enterprise-operator
      
      If your currently installed version is not the latest release, run the following 
      commmand to update your Helm repo:
      
      .. code-block:: sh
      
         helm repo update mongodb
      
      If you don't have the Helm repo installed locally, you can install it by running:
      
      .. code-block:: sh
      
         helm repo add mongodb https://mongodb.github.io/helm-charts
      
   .. step:: Customize your Helm Chart before upgrading it.
      
      To avoid breaking changes, you should ensure that you select the same settings
      as those in your existing deployment. To learn about optional |k8s-op-short| 
      installation settings, see :ref:`Operator Helm Installation Settings <meko-op-install-settings-helm>`.
      
   .. step:: Upgrade the |k8s-op-short|.
      
   .. step:: Clone the MongoDB Enterprise Kubernetes Operator resources repository.
      
      Run the following ``git`` command to clone the required resources:
      
      .. code-block:: sh
      
         git clone https://github.com/mongodb/mongodb-enterprise-kubernetes.git
      
   .. step:: Add custom values to the CRDs.
      
      You can edit the :ref:`MongoDB <k8s-specification>` and :ref:`Ops Manager 
      <k8s-om-specification>` |k8s-crds| to customize your MongoDB 
      deployment as needed.
      
   .. step:: Apply the CRDs to your |k8s| cluster.
      
      Run the following ``kubectl`` command to deploy the CRDs to your |k8s| cluster:
      
      .. code-block::
         
         kubectl apply -f crds.yaml
      
