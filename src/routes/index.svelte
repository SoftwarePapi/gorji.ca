<script context="module">
    import { gql, GraphQLClient } from 'graphql-request'
  
    export const load = async () => {
      const client = new GraphQLClient(
        import.meta.env.VITE_GRAPHQL_API
      )
  
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
      `
  
      const { projects } = await client.request(query)
  
      return {
        props: {
          projects,
        },
      }
    }
  </script>
  
  <script>
    export let projects
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