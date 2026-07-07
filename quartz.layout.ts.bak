import { PageLayout, SharedLayout } from "./quartz/cfg"
import * as Component from "./quartz/components"
import { Options } from "./quartz/components/Explorer"

// customized left nav sorting
const sortFn: Options["sortFn"] = (a, b) => {
  const navOrder = [
    "Field-guide-to-your-first-visit",
    "How-to-pack-for-a-visit",
    "Trans-people-at-the-bathhouse",
    "Bathhouse-basics",
    "Bathhouse-FAQs",
    "Bathhouse-etiquette",
    "Bathhouse-rules",
    "Cruising-in-a-bathhouse",
    "Who-is-the-Bathhouse-Queen",

    "Auntie Queen's Thoughts",
    "Auntie-Queen's-Thoughts/Sniffies-and-the-Baths",
    "Auntie-Queen's-Thoughts/CumUnion-and-the-Baths",
    "Auntie-Queen's-Thoughts/The-Bathhouse-and-STIs",

    "Bathhouse Culture",
    "Bathhouse-Culture/Glossary",
    "Bathhouse-Culture/Kinks,-Fetishes,-and-Subcultures",
    "Bathhouse-Culture/The-History-of-Bathhouses",
    "Bathhouse-Culture/Steamworks-and-Bathhouse-Culture",
    "Bathhouse-Culture/Disco-era-rules-of-the-baths",

    "Bathhouse Reviews",
    "Bathhouse-Reviews/Club-Philly",
    "Bathhouse-Reviews/Crew-Club-DC",
    "Bathhouse-Reviews/Entourage-Las-Vegas",

  ]

  const aSlug = a.data?.slug ?? a.displayName
  const bSlug = b.data?.slug ?? b.displayName

  const aIndex = navOrder.indexOf(aSlug)
  const bIndex = navOrder.indexOf(bSlug)

  if (aIndex !== -1 && bIndex !== -1) return aIndex - bIndex
  if (aIndex !== -1) return -1
  if (bIndex !== -1) return 1

  if (!a.isFolder && b.isFolder) return -1
  if (a.isFolder && !b.isFolder) return 1

  return a.displayName.localeCompare(b.displayName, undefined, {
    numeric: true,
    sensitivity: "base",
  })
}

// Hide any page tagged with explorerexclude from the left nav
const explorerFilter = (node: any) => {
  return node.data?.tags?.includes("explorerexclude") !== true
}

// components shared across all pages
export const sharedPageComponents: SharedLayout = {
  head: Component.Head(),
  header: [],
  afterBody: [],
  footer: Component.Footer(),
}

// components for pages that display a single page (e.g. a single note)
export const defaultContentPageLayout: PageLayout = {
  beforeBody: [
    Component.ConditionalRender({
      component: Component.Breadcrumbs(),
      condition: (page) => page.fileData.slug !== "index",
    }),
    Component.ArticleTitle(),
    Component.ContentMeta(),
    Component.TagList(),
  ],
  left: [
    Component.PageTitle(),
    Component.MobileOnly(Component.Spacer()),
    Component.Flex({
      components: [
        {
          Component: Component.Search(),
          grow: true,
        },
        { Component: Component.Darkmode() },
        { Component: Component.ReaderMode() },
      ],
    }),
    Component.Explorer({
      filterFn: explorerFilter,
      sortFn,
      folderDefaultState: "open",
      useSavedState: false,
    }),
  ],
  right: [
      // remove Graph View and Backlinks from right nav
//    Component.Graph(),
    Component.DesktopOnly(Component.TableOfContents()),
//    Component.Backlinks(),
  ],
}

// components for pages that display lists of pages (e.g. tags or folders)
export const defaultListPageLayout: PageLayout = {
  beforeBody: [Component.Breadcrumbs(), Component.ArticleTitle(), Component.ContentMeta()],
  left: [
    Component.PageTitle(),
    Component.MobileOnly(Component.Spacer()),
    Component.Flex({
      components: [
        {
          Component: Component.Search(),
          grow: true,
        },
        { Component: Component.Darkmode() },
      ],
    }),
    Component.Explorer({
      filterFn: explorerFilter,
      sortFn,
      folderDefaultState: "open",
      useSavedState: false,
    }),
  ],
  right: [],
}
