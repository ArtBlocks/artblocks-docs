# Common Custom Dashboard Mutations

## Introduction

As an Engine partner, you have the option to create a custom artist/admin dashboard. While the majority of your project configuration will occur through on-chain transactions, there are specific off-chain fields that need to be set directly via our GraphQL API.

This documentation outlines the permissions necessary for executing relevant actions and mutations. Please note that a user can only execute a mutation with the artist role for a project if their public address matches the artist address set for the project. A user can execute a mutation with the allowlisted role only if they are the super admin on the project's contract's ACL contract (V3 and up), or if they have been whitelisted on the project's contract (V2 and below).

For all mutations listed in this documentation, the user must include the x-hasura-role header in their request, specifying either artist or allowlisted as the role, as appropriate.


## Actions

Actions are specialized mutations that go beyond simple CRUD operations. Within your custom creator dashboard, you might find the `updateFeatures` and `updateProjectMedia` actions particularly useful.

The `updateFeatures` action initiates a test run of a feature script for a test token. Upon validating that the output aligns with the provided feature fields, it updates both the `feature_fields` and `feature_script` on the project. Both artists and allowlisted users can execute this action. Artists can make updates either before the project is completed, or afterwards, if the allowlisted user has toggled the `enable_artist_update_after_completion` flag on the project's associated features row.

The `updateProjectMedia` action refreshes various media assets linked to a project's tokens. The refreshed media depends on the parameters passed to the action, which may include different formats of preview images and features. This action is accessible to both artists and allowlisted users. However, the execution of this action is rate-limited to once 24 hours for artists.

Here are the parameters accepted by the `updateProjectMedia` action:
- `projectId`: The ID of the project to be updated.
- `features`: A boolean that indicates whether to recalculate features for the project's tokens.
- `render`: A boolean that indicates whether to re-render the preview images for the project.
- `renderVideo`: A boolean that indicates whether to re-render preview videos/gifs for the project.

All these actions are executed via specific mutations in the GraphQL API.


## Tags

Tags and projects share a many-to-many relationship, managed through the `entity_tags` table. Tags serve as non-functional descriptors that can be used to categorize projects. To associate a tag with a project, the `insert_entity_tags` mutation is used.

In the context of an Engine dashboard, you're likely most interested in presentation tags, which can be fetched with the following query:

```
query {
  tags(where: {grouping_name: {_eq: presentation}}) {
    name
  }
}
```

Both the artist and contract admin roles have the permissions to execute the `insert_entity_tags` mutation. Here's an example of how to use this mutation:

```
mutation {
  insert_entity_tags(objects: [{ project_id: "0x...", tag_name: "animated"}])
}
```


## Project

The table below lists permissions for directly updating relevant off-chain fields on the project row. Many of these fields are optional and are intended to enrich the descriptive content on your frontend. Fields marked with an asterisk (*) have a functional impact on the project.

| Field | Artist Permission | Allowlisted Permission | Description
|---|---|---|---|
| `artist_display_notes` | X | X | Contains the artist's intentions for how the artwork should be displayed.
| `link_to_license` | X | X | Provides a link to the copyright license for the project (e.g., "https://creativecommons.org/licenses/by-nc-nd/4.0/").
| `creative_credit` | X | X | Allows artists to acknowledge contributors, inspirations, or other sources of influence.
| `disable_sample_generator` | X | X | Indicates the artist's preference for displaying project previews. Influences whether the "explore possibilities" modal is displayed on the project page on our flagship site.
| `featured_token_id` | X | X | Enables the artist to specify a token ID to feature. Determines the token displayed as the project's cover image on our flagship site.
| `sales_notes` | X | X | Provides specific details about the sales mechanics of the project.
| `charitable_giving_details` | X | X | Outlines any charitable giving aspects associated with the project.
| `render_delay`* | X | X | Sets the delay (in seconds) before our renderer captures a snapshot of the project for preview images.
| `generate_video_assets`* | X | X | Determines whether GIFs and MP4s are generated during individual token refreshes, batch token refreshes, and new token mints.
| `primary_render_type` | X | X | Specifies the preferred format for displaying the project on detail pages.
| `preview_render_type` | X | X | Specifies the preferred format for the project's preview images.
| `artist_interview` | - | X | Provides a link to an interview with the artist.
| `start_date` | - | X | Sets the intended start time of the project, indicating when it will become unpaused and active.

All these fields are updated using the `update_projects_metadata_by_pk` mutation.

---

Please note: In the tables above, 'X' stands for write permissions, and '-' stands for no write permissions.