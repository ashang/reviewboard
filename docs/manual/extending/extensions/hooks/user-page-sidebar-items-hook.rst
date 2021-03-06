.. _user-page-sidebar-items-hook:

========================
UserPageSidebarItemsHook
========================

:py:class:`reviewboard.extensions.hooks.UserPageSidebarItemsHook` can be used
to add items to the sidebar on the user page. These items can contain
anything: Links, images, statistics, or anything else the extension may want
to provide.

Sidebar items are subclasses of
:py:class:`reviewboard.datagrids.sidebar.BaseSidebarItem`. Review Board
provides two built-in items:
:py:class:`reviewboard.datagrids.sidebar.BaseSidebarSection` and
:py:class:`reviewboard.datagrids.sidebar.SidebarNavItem`.

To use the hook, simply instantiate it and pass a list of BaseSidebarItem
subclasses to it. These will then automatically appear in the user page's
sidebar.


Example
=======

.. code-block:: python

    from reviewboard.datagrids.sidebar import (BaseSidebarSection,
                                               SidebarNavItem)
    from reviewboard.extensions.base import Extension
    from reviewboard.extensions.hooks import UserPageSidebarItemsHook


    class SampleSidebarSection(BaseSidebarSection):
        label = 'My Links'

        def get_items(self):
            return [
                SidebarNavItem(label='Link 1',
                               url_name='myvendor_url_name_1',
                               count=10),
                SidebarNavItem(label='Link 2',
                               url_name='myvendor_url_name_2')
            ]


    class SampleExtension(Extension):
        def initialize(self):
            UserPageSidebarItemsHook(self, [SampleSidebarSection])
