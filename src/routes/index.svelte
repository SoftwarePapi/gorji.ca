<script context="module">
  import { gql } from 'graphql-request'
  import { client } from '$lib/graphql-client'

  export const load = async () => {

    const query = gql`
      query GetProjects {
        projects {
          name
          slug
          description
          demo
          sourceCode
          image {
            url
          }
        }
      }
    `;

    const { projects } = await client.request(query);

    return {
      props: {
        projects,
      },
    };
  };
</script>

<script>
  export /**
   * @type {any} */
  let projects;
</script>

{#each projects as project}
  <div>
    <img src={project.image[0].url} alt={project.name} />
    <a href={`/projects/${project.slug}`}>
      <div>
        <h2>{project.name}</h2>
        <p>
          {project.description.slice(0, 80)}...
        </p>
      </div>
    </a>
  </div>
{/each}
