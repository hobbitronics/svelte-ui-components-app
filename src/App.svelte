<script>
  import './mdc/_index.scss'
  import OtherPage from './otherPage.svelte'
  import {
    actions,
    Badge,
    Button,
    Card,
    Checkbox,
    Snackbar,
    setNotice,
    StaticChip,
    CustomCard,
    Form,
    FileDropArea,
    Page,
    TextField,
    TopAppBar,
    Progress,
    Menu,
  } from '@silintl/ui-components'
  import { onMount } from 'svelte'

  let text
  let topics = ['topic1', 'topic2']
  let checked = true
  let toggle = true

  let menuOpen = false

  const menuItems = [
    {
      icon: 'settings',
      label: 'User settings',
      url: '/settings/personal',
    },
    {
      icon: 'logout',
      label: 'Sign out',
      url: '/logout',
    },
  ]

  onMount(() => {
    //actions are for TopAppBar which Drawer uses.
    $actions = [
      {
        icon: 'info_outline',
        label: 'action demo',
        onClick: () => (menuOpen = true),
      },
    ]
  })

  const clickHandler = () => {
    topics = [...topics, text]
    setNotice('You added a topic!')
  }

  const openMenu = () => setNotice("there isn't a menu yet")
</script>

<style>
  .item-menu {
    position: absolute;
    right: 185px;
    top: 25px;
  }
</style>

<OtherPage bind:toggle>
  <!-- <TopAppBar on:nav={openMenu} bgColorIsVariant>{appName}</TopAppBar> -->
  <Page title="test page" layout="grid">
    <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-12">
      <Page.Subheader>This is a template for ui-components</Page.Subheader>

      <Progress.Linear value=".2" />

      <p class="fs-12 gray">
        Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
        how to build Svelte apps.
      </p>
    </div>

    <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
      <Card secondary="secondary text">
        <p class="text-align-center">This is a card</p>

        <Badge bordered color="#FE1234">M</Badge>

        <div class="flex justify-center flex-wrap">
          {#each topics as topic}
            <StaticChip bgColor="yellow">{topic}</StaticChip>
          {/each}
        </div>

        <Form>
          Form
          <TextField label={'Textfield'} bind:value={text} />
        </Form>

        <span slot="actions">
          <Button raised on:click={clickHandler}>add a chip</Button>
          <Button raised on:click={() => (toggle = !toggle)}>open drawer</Button
          >
          <Checkbox label="check this out" bind:checked uppercase />
        </span>
      </Card>
    </div>

    <div class="mdc-layout-grid__cell mdc-layout-grid__cell--span-6">
      <CustomCard
        buttons={[
          {
            label: 'go to ui-components',
            url: 'https://github.com/silinternational/ui-components#readme',
          },
        ]}
        icon="face"
        title="Title goes here"
        alt="graphic"
        src=""
      >
        Add some text content here.
      </CustomCard>

      <FileDropArea
        class="py-4 my-4"
        raised
        on:upload={(e) => console.log(e.detail.get('file'))}
      />
    </div>
    <div class="item-menu">
      <Menu bind:menuOpen {menuItems} class="dib" />
    </div>
  </Page>
</OtherPage>

<Snackbar />
