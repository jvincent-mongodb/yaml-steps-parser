.. procedure::
   :style: normal
      
   .. step:: Select a dashboard.
      
      From your dashboard page, select the dashboard containing the chart
      you wish to make embeddable.
      
   .. step:: Select a chart.
      
      From the dashboard, click :icon-mms:`ellipsis` at the top-right of
      the chart to access its embedding information. Select
      :guilabel:`Embed chart` from the dropdown menu.
      
      .. include:: /includes/fact-charts-in-embedded-dashboards.rst
      
   .. step:: Enable external sharing on the data source.
      
      If you have already enabled external sharing on the data source this
      chart uses, skip this step. If you haven't yet enabled
      embedding on the data source, you can do so now. Click the
      :guilabel:`Configure external sharing` link.
      
   .. step:: Select the :guilabel:`Verified Signature` tab in the dialog window.
   .. step:: Toggle :guilabel:`Enable signed authentication access` to :guilabel:`On`.
   .. step:: Toggle the switch marked :guilabel:`Enable signed authentication access` to :guilabel:`On`.
      The |html| code which appears in the modal window shows the parameters
      which are required to share a chart with authentication enabled, but
      it is not usable as-is. Continue with the subsequent steps to
      enable authenticated access.
      
   .. step:: Go to :guilabel:`Authentication Settings` to acquire an embedding key.
      a. If |charts-short| is not already displayed, click 
         :guilabel:`Charts` in the navigation bar.
      #. Click :guilabel:`Embedding` in the sidebar.
      #. Click the :guilabel:`Authentication Settings` tab.
      
      .. note::
      
         You must be a :ref:`Project Owner <dashboard-permissions>` to
         access the :guilabel:`Authentication Settings` page. As a 
         non-admin user, you can still use embedded charts, but you will 
         need to ask a Project Owner for a key.
      
   .. step:: Generate an embedding key.
      
      Click the :guilabel:`Generate New Key` button to create a new
      embedding key. Store the key in a safe place.
      
      .. warning::
      
         If you generate a new key, any previous keys become invalid.
         Ensure that all the existing shared charts that use the old key
         are updated to use the new key.
      
   .. step:: Create the server-side code necessary for a verified signature.
      Generating a verified signature to accompany data requests from shared
      charts with authentication enabled requires server-side code. The
      verified signature creates a payload by generating a
      :wikipedia:`HMAC </HMAC>` from your embedding key, a timestamp, and
      identifying data from your chart. The verified signature is valid for
      a limited time period specified in your server-side code.
      
      Code examples demonstrating how to generate a verified
      signature are available for the following languages and platforms:
      
      - :github:`Node.js </mongodb/charts-embedding-examples/tree/master/node>`
      - :github:`C# </mongodb/charts-embedding-examples/tree/master/c-sharp>`
      - :github:`Java </mongodb/charts-embedding-examples/tree/master/java>`
      - :github:`Python </mongodb/charts-embedding-examples/tree/master/python>`
      - :github:`MongoDB Stitch </mongodb/charts-embedding-examples/tree/master/stitch>`
      
