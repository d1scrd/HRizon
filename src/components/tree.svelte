<script>
    import { onMount } from 'svelte';
  
    let tree;
    let data = {
      id: 'ms',
      data: {
        id: 'ms',
        imageURL: 'https://i.pravatar.cc/300?img=68',
        name: 'Margret Swanson',
      },
      options: {
        nodeBGColor: '#cdb4db',
        nodeBGColorHover: '#cdb4db',
      },
      children: [
        {
          id: 'mh',
          data: {
            id: 'mh',
            imageURL: 'https://i.pravatar.cc/300?img=69',
            name: 'Mark Hudson',
          },
          options: {
            nodeBGColor: '#ffafcc',
            nodeBGColorHover: '#ffafcc',
          },
          children: [
            {
              id: 'kb',
              data: {
                id: 'kb',
                imageURL: 'https://i.pravatar.cc/300?img=65',
                name: 'Karyn Borbas',
              },
              options: {
                nodeBGColor: '#f8ad9d',
                nodeBGColorHover: '#f8ad9d',
              },
            },
            {
              id: 'cr',
              data: {
                id: 'cr',
                imageURL: 'https://i.pravatar.cc/300?img=60',
                name: 'Chris Rup',
              },
              options: {
                nodeBGColor: '#c9cba3',
                nodeBGColorHover: '#c9cba3',
              },
            },
          ],
        },
        {
          id: 'cs',
          data: {
            id: 'cs',
            imageURL: 'https://i.pravatar.cc/300?img=59',
            name: 'Chris Lysek',
          },
          options: {
            nodeBGColor: '#00afb9',
            nodeBGColorHover: '#00afb9',
          },
          children: [
            {
              id: 'Noah_Chandler',
              data: {
                id: 'Noah_Chandler',
                imageURL: 'https://i.pravatar.cc/300?img=57',
                name: 'Noah Chandler',
              },
              options: {
                nodeBGColor: '#84a59d',
                nodeBGColorHover: '#84a59d',
              },
            },
            {
              id: 'Felix_Wagner',
              data: {
                id: 'Felix_Wagner',
                imageURL: 'https://i.pravatar.cc/300?img=52',
                name: 'Felix Wagner',
              },
              options: {
                nodeBGColor: '#0081a7',
                nodeBGColorHover: '#0081a7',
              },
            },
          ],
        },
      ],
    };
  
    let currentNodeId = null;
    let editName = '';
    let editImageURL = '';
  
    function openEditModal(nodeId) {
      console.log(`Opening edit modal for node ID: ${nodeId}`);
      currentNodeId = nodeId;
      const node = findNodeById(data, nodeId);
      if (node) {
        editName = node.data.name;
        editImageURL = node.data.imageURL;
        document.getElementById('editModal').style.display = 'block';
      } else {
        console.error(`Node with ID ${nodeId} not found`);
      }
    }
  
    function closeEditModal() {
      document.getElementById('editModal').style.display = 'none';
    }
  
    function saveNode() {
      const nodeId = currentNodeId;
      updateNodeData(data, nodeId, { name: editName, imageURL: editImageURL });
      closeEditModal();
      tree.render(data);
    }
  
    function findNodeById(node, id) {
      if (node.id === id) return node;
      if (node.children) {
        for (const child of node.children) {
          const result = findNodeById(child, id);
          if (result) return result;
        }
      }
      return null;
    }
  
    function updateNodeData(node, id, newData) {
      const targetNode = findNodeById(node, id);
      if (targetNode) {
        targetNode.data = { ...targetNode.data, ...newData };
      }
    }
  
    onMount(() => {
      window.openEditModal = openEditModal;
  
      const nodeTemplate = (content) => {
        return `
          <div style='display: flex;flex-direction: column;gap: 10px;justify-content: center;align-items: center;height: 100%;'>
            <img style='width: 50px;height: 50px;border-radius: 50%;' src='${content.imageURL}' alt='' />
            <div style="font-weight: bold; font-family: Arial; font-size: 14px">${content.name}</div>
            <button onclick="openEditModal('${content.id}')">Edit</button>
          </div>
        `;
      };
  
      const options = {
        contentKey: 'data',
        width: 700,
        height: 700,
        nodeWidth: 150,
        nodeHeight: 100,
        fontColor: '#fff',
        borderColor: '#333',
        childrenSpacing: 100,
        siblingSpacing: 30,
        direction: 'top',
        enableExpandCollapse: true,
        nodeTemplate: (content) => nodeTemplate(content),
        canvasStyle: 'border: 1px solid black; background: #f6f6f6;',
        enableToolbar: true,
      };
  
      tree = new ApexTree(document.getElementById('svg-tree'), options);
      tree.render(data);
    });
  </script>
  
  <div id="svg-tree"></div>
  
  <!-- Modal -->
  <div id="editModal" style="display:none; position:fixed; top:50%; left:50%; transform:translate(-50%, -50%); background:white; padding:20px; border:1px solid #ccc;">
    <h2>Edit Node</h2>
    <form id="editForm">
      <input type="hidden" id="editNodeId">
      <label for="editName">Name:</label>
      <input type="text" bind:value={editName} id="editName" name="editName"><br><br>
      <label for="editImageURL">Image URL:</label>
      <input type="text" bind:value={editImageURL} id="editImageURL" name="editImageURL"><br><br>
      <button type="button" on:click={saveNode}>Save</button>
      <button type="button" on:click={closeEditModal}>Cancel</button>
    </form>
  </div>
  
  <style>
    #svg-tree {
      margin: 0 auto;
    }
  </style>
  